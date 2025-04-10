
# SQL Date and Time Functions Guide

This markdown covers the usage and examples of important SQL date/time conversion functions such as `CAST`, `CONVERT`, `STR_TO_DATE()`, and `DATE_FORMAT()`. It also includes format specifiers and commonly asked interview questions.

---

## 🔄 1. CAST() Function

**Purpose**: Used to convert one data type to another.

**Syntax**:
```sql
CAST(expression AS target_data_type)
```

**Example**:
```sql
SELECT CAST('2025-04-10' AS DATE) AS formatted_date;
SELECT CAST(123.45 AS INT) AS integer_value;
```

---

## 🔁 2. CONVERT() Function (T-SQL / SQL Server specific)

**Purpose**: Also used to convert between data types, and more flexible with date formatting.

**Syntax**:
```sql
CONVERT(data_type(length), expression, style)
```

**Example**:
```sql
SELECT CONVERT(VARCHAR, GETDATE(), 103) AS formatted_date; -- returns DD/MM/YYYY
SELECT CONVERT(DATE, '2025-04-10') AS converted_date;
```

**Note**: Style code like `103` means British/French date format (DD/MM/YYYY).

---

## 📥 3. STR_TO_DATE() Function (MySQL)

**Purpose**: Parses a string into a date based on the given format.

**Syntax**:
```sql
STR_TO_DATE(string, format)
```

**Example**:
```sql
SELECT STR_TO_DATE('10-04-2025', '%d-%m-%Y') AS parsed_date;
```

---

## 📤 4. DATE_FORMAT() Function (MySQL)

**Purpose**: Formats a date value into a readable string using a specific format.

**Syntax**:
```sql
DATE_FORMAT(date, format)
```

**Example**:
```sql
SELECT DATE_FORMAT(NOW(), '%W, %M %d, %Y') AS formatted;
-- Output: Thursday, April 10, 2025
```

---

## 📆 Format Specifiers (MySQL Style)

| Format Code | Description                    | Example         |
|-------------|--------------------------------|-----------------|
| `%Y`        | Four-digit year                | `2025`          |
| `%y`        | Two-digit year                 | `25`            |
| `%M`        | Full month name                | `April`         |
| `%m`        | Month (01-12)                  | `04`            |
| `%d`        | Day of month (01-31)           | `10`            |
| `%e`        | Day of month (1-31)            | `10`            |
| `%W`        | Full weekday name              | `Thursday`      |
| `%a`        | Abbreviated weekday name       | `Thu`           |
| `%H`        | Hour (00-23)                   | `15`            |
| `%h` / `%I` | Hour (01-12)                   | `03`            |
| `%i`        | Minutes (00-59)                | `30`            |
| `%s` / `%S` | Seconds (00-59)                | `45`            |
| `%p`        | AM or PM                       | `PM`            |
| `%b`        | Abbreviated month name         | `Apr`           |

---

## 🔍 Use Cases

### ✅ Convert string to date:
```sql
SELECT STR_TO_DATE('2025-10-04', '%Y-%m-%d');
```

### ✅ Format current date nicely:
```sql
SELECT DATE_FORMAT(NOW(), '%W, %d %M %Y');
```

### ✅ Cast numbers:
```sql
SELECT CAST('123.456' AS DECIMAL(6,2)) AS value;
```

### ✅ Format date using CONVERT (SQL Server):
```sql
SELECT CONVERT(VARCHAR, GETDATE(), 113); -- DD Mon YYYY HH:MM:SS
```

---

## 💼 Interview Questions and Answers

### Q1: What is the difference between CAST and CONVERT in SQL?
**A**: Both are used for type conversion. `CAST` is ANSI SQL standard; `CONVERT` is specific to SQL Server and provides additional formatting options for dates.

---

### Q2: How do you change a string like '10/04/2025' to a date?
**A** (MySQL):
```sql
SELECT STR_TO_DATE('10/04/2025', '%d/%m/%Y');
```

---

### Q3: How can you extract the month name from a date?
**A**:
```sql
SELECT DATE_FORMAT('2025-04-10', '%M');
-- Output: April
```

---

### Q4: What is the output of `%m` vs `%M` in DATE_FORMAT?
**A**:
- `%m`: numeric month (e.g., `04`)
- `%M`: full month name (e.g., `April`)

---

### Q5: How do you display the current date in `DD-MM-YYYY` format?
**A**:
```sql
SELECT DATE_FORMAT(NOW(), '%d-%m-%Y');
```

---

### Q6: How can you cast a float number to an integer?
**A**:
```sql
SELECT CAST(123.45 AS INT); -- Output: 123
```

---

### Q7: When should STR_TO_DATE be used?
**A**: Use `STR_TO_DATE` when you have a date stored as a string and you want to convert it into a `DATE` or `DATETIME` type using a specific format.

---

### Q8: How to find day name of a given date?
**A**:
```sql
SELECT DATE_FORMAT('2025-04-10', '%W');
-- Output: Thursday
```

---

### Q9: What is the format specifier for 24-hour clock?
**A**:
- `%H`: Hour in 24-hour format (00–23)

---

### Q10: Convert '25-April-2025' to date format:
**A**:
```sql
SELECT STR_TO_DATE('25-April-2025', '%d-%M-%Y');
```

---

## 📚 References

- [MySQL DATE_FORMAT() Docs](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html)
- [T-SQL CONVERT() Docs](https://learn.microsoft.com/en-us/sql/t-sql/functions/cast-and-convert-transact-sql)

---

## 🧠 Pro Tip

Always check your database type before using `STR_TO_DATE()` or `CONVERT()`, since these functions are specific to MySQL and SQL Server respectively.
