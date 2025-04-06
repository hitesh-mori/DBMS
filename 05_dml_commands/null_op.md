

# NULL Handling in SQL: `NULL`, `IS NULL`, `IS NOT NULL`

---

## 📘 Introduction

In SQL, `NULL` represents **missing**, **unknown**, or **undefined** values. It is **not equivalent to 0, empty string (''), or false**.

---

## 🔹 1. `NULL`

### ✅ Definition:
- A special marker used to indicate that a **data value does not exist** in the database.

### 🔍 Example:
```sql
INSERT INTO students (id, name, email) VALUES (1, 'Alice', NULL);
```

---

## 🔹 2. `IS NULL`

### ✅ Definition:
Used in the `WHERE` clause to **check if a value is NULL**.

### 🔍 Example:
```sql
SELECT * FROM students
WHERE email IS NULL;
```

---

## 🔹 3. `IS NOT NULL`

### ✅ Definition:
Used to **filter out** rows where the value is not NULL.

### 🔍 Example:
```sql
SELECT * FROM students
WHERE email IS NOT NULL;
```

---

## ⚠️ Note:
You **CANNOT** use `=` or `!=` to compare `NULL`. Always use `IS NULL` or `IS NOT NULL`.

```sql
-- ❌ Incorrect
WHERE email = NULL;

-- ✅ Correct
WHERE email IS NULL;
```

---

## 🧠 Hard Interview Questions with Answers

---

### 1. **What is the difference between `NULL` and an empty string `''`?**

**Answer:**
- `NULL` means **no value** or **unknown**.
- `''` is a **known empty value**, i.e., a string of length 0.

---

### 2. **Why can’t you use `=` to compare with `NULL`?**

**Answer:**
Because `NULL` is **not a value**; it's a **marker** for "missing information". `NULL = NULL` results in `UNKNOWN`, not `TRUE`.

---

### 3. **What does `NULL + 10` return?**

**Answer:**
It returns `NULL`. Any arithmetic or operation with `NULL` results in `NULL`.

---

### 4. **Write a query to find all students who have not provided their email.**

**Answer:**
```sql
SELECT * FROM students WHERE email IS NULL;
```

---

### 5. **Is `NULL = NULL` true?**

**Answer:**
**No.** In SQL, `NULL = NULL` evaluates to `UNKNOWN`. Use `IS NULL` instead.

---

### 6. **How do you count only non-null entries in a column?**

**Answer:**
```sql
SELECT COUNT(email) FROM students;
```
`COUNT(column)` ignores `NULL` values automatically.

---

### 7. **How do you include NULLs in a `GROUP BY` or `ORDER BY` clause?**

**Answer:**
SQL will group or order rows with `NULL` as a **distinct group/value**. To control behavior, use:
```sql
ORDER BY column_name IS NULL, column_name;
```

---

### 8. **How do you handle NULLs in comparisons in a `JOIN`?**

**Answer:**
Use `IS NULL` explicitly, or use `OUTER JOIN` to include unmatched `NULL` values.

---

### 9. **What is `COALESCE()` and how is it used with `NULL`?**

**Answer:**
`COALESCE(expr1, expr2, ...)` returns the **first non-null value**.

```sql
SELECT COALESCE(email, 'not provided') AS email_status FROM students;
```

---

### 10. **What is the result of this query?**

```sql
SELECT CASE WHEN NULL = NULL THEN 'YES' ELSE 'NO' END;
```

**Answer:**
Returns `NO`, because `NULL = NULL` evaluates to `UNKNOWN`.

---

## ✅ Summary

| Keyword       | Description                            |
|---------------|----------------------------------------|
| `NULL`        | Missing or undefined value             |
| `IS NULL`     | Checks if a column has `NULL`          |
| `IS NOT NULL` | Checks if a column has non-null value  |
| `=` / `!=`    | ❌ Don't use with `NULL`               |

---

## 🛠️ Best Practices

- Always use `IS NULL` / `IS NOT NULL` for null checks.
- Avoid using `=` with `NULL`.
- Use `COALESCE()` or `IFNULL()` to replace NULLs during select.

---