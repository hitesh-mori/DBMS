
# 📘 SQL Data Type Differences

SQL provides a variety of data types to store different kinds of data. Some data types seem similar but behave differently in terms of **storage, performance, and use-case**.

Below is a detailed comparison of the most commonly confused SQL data types.

---

## 1. 🔡 `CHAR(n)` vs `VARCHAR(n)`

| Feature         | `CHAR(n)`                        | `VARCHAR(n)`                          |
|-----------------|----------------------------------|----------------------------------------|
| Definition      | Fixed-length character string    | Variable-length character string       |
| Padding         | Padded with spaces to `n` length | No padding                             |
| Storage         | Always uses `n` bytes            | Uses actual length + 1 or 2 bytes overhead |
| Performance     | Faster for fixed-length strings  | More efficient for varied-length strings |
| Use Case        | Codes, fixed-length fields       | Names, addresses, variable text        |

> ⚠️ `CHAR(10)` stores `'abc'` as `'abc       '`, while `VARCHAR(10)` stores it as `'abc'`.

---

## 2. 🔢 `DECIMAL(p, s)` vs `FLOAT`

| Feature          | `DECIMAL(p, s)`                           | `FLOAT` / `REAL`                         |
|------------------|-------------------------------------------|------------------------------------------|
| Precision        | Fixed and exact                           | Approximate and may cause rounding errors|
| Accuracy         | High — used in financial calculations     | Lower — suitable for scientific data     |
| Storage          | More storage for higher precision         | Less storage, faster operations          |
| Use Case         | Money, banking, accounting                | Scientific calculations, sensor data     |

> Example:  
> `DECIMAL(5,2)` stores values like `123.45` exactly, while `FLOAT` might store `123.45` as `123.4499969482`.

---

## 3. 📅 `DATE` vs `DATETIME` vs `TIMESTAMP`

| Feature       | `DATE`         | `DATETIME`                    | `TIMESTAMP`                      |
|----------------|----------------|-------------------------------|----------------------------------|
| Stores         | Only date (`YYYY-MM-DD`) | Date & time (`YYYY-MM-DD HH:MM:SS`) | Date & time with time zone offset (sometimes in UTC) |
| Size (MySQL)   | 3 bytes        | 8 bytes                       | 4 bytes (varies by DBMS)         |
| Timezone aware | ❌ No          | ❌ No                          | ✅ Yes                           |
| Range          | 1000-9999      | 1000-9999                     | 1970-2038                        |
| Use Case       | Birth dates, joining dates | Audit logs, records           | Server-based time tracking       |

---

## 4. 🎯 `INT` vs `BIGINT` vs `SMALLINT` vs `TINYINT`

| Type       | Storage | Min Value               | Max Value               |
|------------|---------|--------------------------|--------------------------|
| `TINYINT`  | 1 byte  | 0 to 255 (unsigned)      | -128 to 127 (signed)     |
| `SMALLINT` | 2 bytes | 0 to 65,535 (unsigned)   | -32,768 to 32,767 (signed)|
| `INT`      | 4 bytes | 0 to 4,294,967,295       | -2,147,483,648 to 2,147,483,647 |
| `BIGINT`   | 8 bytes | Very large values        |                         |

> Choose the smallest integer type that fits your data to save space.

---

## 5. 🔗 `TEXT` vs `VARCHAR(n)`

| Feature        | `TEXT`                          | `VARCHAR(n)`                 |
|----------------|----------------------------------|-------------------------------|
| Length         | Can store very long text (up to 2GB in some DBMS) | Up to defined limit (e.g., 255, 65535) |
| Indexing       | Not fully indexable             | Fully indexable               |
| Performance    | Slightly slower, stored off-page | Faster, stored inline         |
| Use Case       | Articles, comments, descriptions | Names, emails, titles         |

---

## 6. 🎭 `BOOLEAN` vs `BIT`

| Feature       | `BOOLEAN`                     | `BIT`                    |
|---------------|-------------------------------|--------------------------|
| Stores        | TRUE/FALSE                    | 0 or 1 (can store multiple bits) |
| Storage       | 1 byte (or DBMS-specific)     | 1 bit (packed)           |
| Compatibility | Standard SQL supported        | DBMS-specific behavior   |
| Use Case      | Flags, logical checks         | Compact bit storage      |

---

## 7. 📦 `ENUM` vs `VARCHAR`

| Feature         | `ENUM`                                     | `VARCHAR`                         |
|------------------|---------------------------------------------|------------------------------------|
| Values Allowed   | Predefined list of values                  | Any value up to defined length     |
| Storage          | Internally stored as index                 | Stored as string                   |
| Flexibility      | Less flexible (needs ALTER to add)         | Fully flexible                     |
| Use Case         | Status (`active`, `inactive`, etc.)        | User input, names, etc.            |

---
