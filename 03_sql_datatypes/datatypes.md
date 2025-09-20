
# 📘 SQL Data Types – Complete Guide

SQL data types define the type of data a column can hold. They vary slightly between database systems (e.g., MySQL, PostgreSQL, Oracle), but the core concepts remain consistent.

---

## 🔷 1. **String (Character) Data Types**

| Data Type    | Description                         | Min Size       | Max Size                           | Use Case                        |
|--------------|-------------------------------------|----------------|------------------------------------|----------------------------------|
| `CHAR(n)`    | Fixed-length character string       | 1 character    | MySQL: 255, PostgreSQL: 10,485     | Country codes, gender, status   |
| `VARCHAR(n)` | Variable-length string              | 1 character    | MySQL: 65,535 bytes                | Names, emails, addresses        |
| `TEXT`       | Large text field                    | 1 character    | MySQL: 65,535 characters           | Long-form text (blogs, comments)|
| `TINYTEXT`   | Very small text                     | 1 character    | 255 bytes                          | Short descriptions              |
| `MEDIUMTEXT` | Medium-length text                  | 1 character    | 16,777,215 characters              | Articles, documents             |
| `LONGTEXT`   | Very large text                     | 1 character    | 4,294,967,295 characters           | Books, logs, large JSON blobs   |
| `ENUM`       | String object with predefined values| —              | 65,535 elements (in MySQL)         | Status (e.g., 'active', 'pending')|

> 📝 Note: `CHAR` is **padded** with spaces, `VARCHAR` is not.

---

## 🔶 2. **Numeric Data Types**

### 🔸 Integers

| Data Type     | Description            | Range (Signed)                    | Storage | Use Case                    |
|---------------|------------------------|----------------------------------|---------|-----------------------------|
| `TINYINT`     | Very small int         | -128 to 127                      | 1 byte  | Age, flags, small counters  |
| `SMALLINT`    | Small int              | -32,768 to 32,767                | 2 bytes | Years, counts               |
| `MEDIUMINT`   | Medium int             | -8,388,608 to 8,388,607          | 3 bytes | Temperature, IDs            |
| `INT` / `INTEGER` | Normal int         | -2,147,483,648 to 2,147,483,647  | 4 bytes | IDs, numeric fields         |
| `BIGINT`      | Large int              | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | 8 bytes | Financial data, counters |

### 🔸 Decimal / Floating Point

| Data Type     | Description                   | Precision              | Storage      | Use Case                |
|---------------|-------------------------------|------------------------|--------------|-------------------------|
| `DECIMAL(p,s)`| Fixed-point (exact)           | Up to 65 digits        | Varies       | Money, financial values |
| `NUMERIC(p,s)`| Same as `DECIMAL`             | Up to 65 digits        | Varies       | Prices, rates           |
| `FLOAT`       | Approximate floating-point    | ~7 digits              | 4 bytes      | Scientific, measurements|
| `DOUBLE`      | Double-precision float        | ~15 digits             | 8 bytes      | High-precision calc     |
| `REAL`        | Alias for `FLOAT`/`DOUBLE`    | System dependent       | 4 or 8 bytes | Approximate values      |

---

## 🔷 3. **Date and Time Data Types**

| Data Type     | Description                | Format                  | Range                             | Use Case               |
|---------------|----------------------------|--------------------------|------------------------------------|------------------------|
| `DATE`        | Date only                  | `YYYY-MM-DD`             | 1000-01-01 to 9999-12-31           | Birthdate, schedule    |
| `TIME`        | Time only                  | `HH:MM:SS`               | -838:59:59 to 838:59:59            | Duration, time logs    |
| `DATETIME`    | Date and time              | `YYYY-MM-DD HH:MM:SS`    | 1000-01-01 00:00:00 to 9999-12-31 23:59:59 | Timestamping        |
| `TIMESTAMP`   | Auto-updating timestamp    | Unix Epoch-based         | 1970-01-01 to 2038-01-19 (MySQL)   | Row creation/update    |
| `YEAR`        | Year only                  | `YYYY`                   | 1901 to 2155                       | Year of manufacture    |


---

# 📅 MySQL `DATE_FORMAT()` Specifiers

| Code             | Output Example | Meaning                                       |
| ---------------- | -------------- | --------------------------------------------- |
| **%d**           | `21`           | Day of month (01–31, zero-padded)             |
| **%e**           | `21`           | Day of month (1–31, no leading zero)          |
| **%a**           | `Sat`          | Abbreviated weekday name                      |
| **%W**           | `Saturday`     | Full weekday name                             |
| **%b**           | `Jul`          | Abbreviated month name                        |
| **%M**           | `July`         | Full month name                               |
| **%m**           | `07`           | Month number (01–12, zero-padded)             |
| **%c**           | `7`            | Month number (1–12, no leading zero)          |
| **%y**           | `12`           | Year (last 2 digits)                          |
| **%Y**           | `2012`         | Year (4 digits)                               |
| **%H**           | `23`           | Hour (00–23, 24-hour clock)                   |
| **%h** or **%I** | `11`           | Hour (01–12, 12-hour clock)                   |
| **%p**           | `AM` / `PM`    | Meridian indicator                            |
| **%i**           | `59`           | Minutes (00–59)                               |
| **%s** or **%S** | `45`           | Seconds (00–59)                               |
| **%f**           | `123456`       | Microseconds (000000–999999)                  |
| **%T**           | `23:59:59`     | 24-hour time (`%H:%i:%s`)                     |
| **%r**           | `11:59:59 PM`  | 12-hour time (`%h:%i:%s %p`)                  |
| **%j**           | `172`          | Day of year (001–366)                         |
| **%U**           | `25`           | Week number (Sunday first day of week, 00–53) |
| **%u**           | `25`           | Week number (Monday first day of week, 00–53) |
| **%V**           | `25`           | Week number (ISO 8601, with `%X`)             |
| **%x**           | `2012`         | Year for week (Monday first)                  |
| **%X**           | `2012`         | Year for week (Sunday first)                  |

---


## 🔶 4. **Boolean Data Type**

| Data Type | Description            | Values    | Storage   | Use Case         |
|-----------|------------------------|-----------|-----------|------------------|
| `BOOLEAN` | True or false          | 0 (false), 1 (true) | 1 byte (TINYINT) | Status flags, toggles |

---

## 🔷 5. **Binary Data Types**

Used for storing images, files, encrypted data.

| Data Type     | Description                  | Max Size                   |
|---------------|------------------------------|----------------------------|
| `BINARY(n)`   | Fixed-length binary string   | 255 bytes                  |
| `VARBINARY(n)`| Variable-length binary string| 65,535 bytes               |
| `TINYBLOB`    | Small binary object          | 255 bytes                  |
| `BLOB`        | Binary Large Object          | 65,535 bytes               |
| `MEDIUMBLOB`  | Medium binary object         | 16 MB                      |
| `LONGBLOB`    | Large binary object          | 4 GB                       |

---

## 🧮 Choosing the Right Data Type

| Data Type       | Best For                                  |
|------------------|-------------------------------------------|
| `CHAR(n)`        | Fixed-size values like gender, codes      |
| `VARCHAR(n)`     | Names, emails, anything variable-length   |
| `TEXT`           | Long-form unstructured text               |
| `INT`/`BIGINT`   | Numeric IDs, count values                 |
| `DECIMAL`        | Financial/accurate calculations           |
| `DATE/DATETIME`  | Timestamps, logs, time tracking           |
| `BOOLEAN`        | Status, feature flags                     |
| `BLOB`           | Images, files, media                      |

---

## 📏 Max Size Summary (MySQL)

| Type        | Max Size            |
|-------------|---------------------|
| `VARCHAR`   | ~65,535 bytes (depends on row size & encoding) |
| `TEXT`      | 65,535 characters   |
| `BLOB`      | 65,535 bytes        |
| `INT`       | 4 bytes             |
| `BIGINT`    | 8 bytes             |
| `DECIMAL`   | Up to 65 digits     |
| `TIMESTAMP` | ~2038 cutoff (MySQL) |

---

## 💡 Pro Tips

- Always choose the **smallest type** that can handle your data.
- Prefer `VARCHAR` over `CHAR` unless you need fixed-length.
- Use `DECIMAL` instead of `FLOAT` for **money** to avoid rounding issues.
- Use `TIMESTAMP` with `DEFAULT CURRENT_TIMESTAMP` for auto-tracking time.
- Watch out for **storage limits** on rows and indexes!

---
