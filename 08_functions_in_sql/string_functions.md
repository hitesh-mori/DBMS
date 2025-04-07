
# 📘 SQL String Functions: Detailed Guide

This document explains all major **SQL String Functions** with syntax, practical examples, and interview-level questions.

---

## 📋 Table of Contents
1. [ASCII](#ascii)
2. [CONCAT](#concat)
3. [CONCAT_WS](#concat_ws)
4. [LENGTH / CHAR_LENGTH](#length--char_length)
5. [UPPER / UCASE](#upper--ucase)
6. [LOWER / LCASE](#lower--lcase)
7. [REPLACE](#replace)
8. [REVERSE](#reverse)
9. [SUBSTRING / SUBSTR](#substring--substr)
10. [TRIM (LEADING / TRAILING / BOTH)](#trim)
11. [LEFT](#left)
12. [RIGHT](#right)
13. [💡 Toughest Interview Questions](#💡-toughest-interview-questions)

---

## `ASCII`

**Description:** Returns the ASCII value of the first character in a string.

**Syntax:**
```sql
SELECT ASCII(string);
```

**Example:**
```sql
SELECT ASCII('A');  -- Result: 65
```

---

## `CONCAT`

**Description:** Joins two or more strings together.

**Syntax:**
```sql
SELECT CONCAT(string1, string2, ...);
```

**Example:**
```sql
SELECT CONCAT('Hello', ' ', 'World');  -- Result: 'Hello World'
```

---

## `CONCAT_WS`

**Description:** Joins strings with a separator. `WS` stands for With Separator.

**Syntax:**
```sql
SELECT CONCAT_WS(separator, string1, string2, ...);
```

**Example:**
```sql
SELECT CONCAT_WS('-', '2025', '04', '07');  -- Result: '2025-04-07'
```

---

## `LENGTH` / `CHAR_LENGTH`

**Description:** 
- `LENGTH()` returns the number of **bytes**.
- `CHAR_LENGTH()` returns the number of **characters**.

**Syntax:**
```sql
SELECT LENGTH(string);
SELECT CHAR_LENGTH(string);
```

**Example:**
```sql
SELECT LENGTH('abc');       -- Result: 3
SELECT CHAR_LENGTH('abc');  -- Result: 3
```

---

## `UPPER` / `UCASE`

**Description:** Converts all characters in a string to uppercase.

**Syntax:**
```sql
SELECT UPPER(string);
SELECT UCASE(string);
```

**Example:**
```sql
SELECT UPPER('hello');  -- Result: 'HELLO'
```

---

## `LOWER` / `LCASE`

**Description:** Converts all characters in a string to lowercase.

**Syntax:**
```sql
SELECT LOWER(string);
SELECT LCASE(string);
```

**Example:**
```sql
SELECT LOWER('HELLO');  -- Result: 'hello'
```

---

## `REPLACE`

**Description:** Replaces all occurrences of a substring with another substring.

**Syntax:**
```sql
SELECT REPLACE(original_string, from_substring, to_substring);
```

**Example:**
```sql
SELECT REPLACE('abcabc', 'a', 'x');  -- Result: 'xbcxbc'
```

---

## `REVERSE`

**Description:** Reverses the characters in a string.

**Syntax:**
```sql
SELECT REVERSE(string);
```

**Example:**
```sql
SELECT REVERSE('hello');  -- Result: 'olleh'
```

---

## `SUBSTRING` / `SUBSTR`

**Description:** Extracts a part of the string starting from a given position with optional length.

**Syntax:**
```sql
SELECT SUBSTRING(string, start_position, length);
SELECT SUBSTR(string, start_position, length);
```

**Example:**
```sql
SELECT SUBSTRING('abcdef', 2, 3);  -- Result: 'bcd'
```

---

## `TRIM`

**Description:** Removes specified characters from a string.

**Syntax:**
```sql
SELECT TRIM([LEADING | TRAILING | BOTH] 'char' FROM string);
```

**Examples:**
```sql
SELECT TRIM('   hello   ');                    -- Result: 'hello'
SELECT TRIM(BOTH 'x' FROM 'xxhelloxx');        -- Result: 'hello'
SELECT TRIM(LEADING 'x' FROM 'xxhelloxx');     -- Result: 'helloxx'
SELECT TRIM(TRAILING 'x' FROM 'xxhelloxx');    -- Result: 'xxhello'
```

---

## `LEFT`

**Description:** Returns the first N characters from the left.

**Syntax:**
```sql
SELECT LEFT(string, number_of_characters);
```

**Example:**
```sql
SELECT LEFT('abcdef', 3);  -- Result: 'abc'
```

---

## `RIGHT`

**Description:** Returns the last N characters from the right.

**Syntax:**
```sql
SELECT RIGHT(string, number_of_characters);
```

**Example:**
```sql
SELECT RIGHT('abcdef', 2);  -- Result: 'ef'
```

---

## 💡 Toughest Interview Questions

1. **Q1:** How would you find and remove duplicate words in a string column using SQL string functions?
   > _Hint: Use `REPLACE`, `TRIM`, and `LIKE` with `CROSS APPLY` or CTE if supported._

2. **Q2:** Write a query to reverse each word in a sentence but keep the word order same.
   > _Advanced use of `REVERSE`, `SUBSTRING_INDEX`, `REGEXP_SUBSTR` (MySQL 8+), or use recursive CTEs._

3. **Q3:** How can you extract the domain name from an email column using SQL string functions?
   ```sql
   SELECT SUBSTRING(email, LOCATE('@', email) + 1) FROM users;
   ```

4. **Q4:** You have a column with comma-separated values. Write a query to split them into separate rows.
   > _Use recursive CTE or `STRING_SPLIT()` in SQL Server or `REGEXP_SUBSTR()` in MySQL._

5. **Q5:** Detect palindromes using SQL (a string that reads the same forward and backward).
   ```sql
   SELECT name
   FROM words
   WHERE name = REVERSE(name);
   ```

