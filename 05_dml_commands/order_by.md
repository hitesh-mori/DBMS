
## 📘 `ORDER BY` in SQL – Complete Guide

### 🔹 1. Basic Syntax

```sql
SELECT * FROM table_name
ORDER BY column_name [ASC | DESC];
```

- `ASC` – Ascending (default)
- `DESC` – Descending

---

### 🔹 2. Order by One Column

```sql
SELECT * FROM teacher
ORDER BY salary;
-- This sorts by salary in ascending order (lowest first)
```

---

### 🔹 3. Order by Multiple Columns

```sql
SELECT * FROM teacher
ORDER BY dep_id ASC, salary DESC;
-- First sorts by department, then salary (highest first) within each department
```

---

### 🔹 4. Order By with WHERE Clause

```sql
SELECT * FROM teacher
WHERE salary IS NOT NULL
ORDER BY salary DESC;
```

You can always use `ORDER BY` **after** `WHERE` clause. SQL execution order matters:
- `WHERE` filters rows
- `ORDER BY` sorts the filtered results

---

### 🔹 5. Default Sorting Order?

✅ **Ascending (`ASC`) is default** if not specified.

```sql
SELECT * FROM student ORDER BY name; 
-- Same as ORDER BY name ASC
```

---

### 🔹 6. ORDER BY with NULLs

```sql
SELECT * FROM teacher ORDER BY salary;
```

- In MySQL: `NULL`s are treated as **lowest** in ascending, **highest** in descending.

---

## 💡 INTERVIEW THEORY

| Concept                | Detail                                                                 |
|------------------------|-------------------------------------------------------------------------|
| Can you use `ORDER BY` without `SELECT *`? | ✅ Yes, you can use specific columns only |
| Does `ORDER BY` improve performance?        | ❌ No. It can **slow down** large result sets |
| Is `ORDER BY` mandatory after `GROUP BY`?   | ❌ No. But useful to control final output order |
| Can indexes help `ORDER BY`?                | ✅ Yes, in some cases when query planner can use it |
| Is sort stable in SQL?                      | ❌ Not guaranteed unless explicitly specified |

---

## 💥 HARD INTERVIEW QUESTIONS

### Q1: What will happen if two rows have the same value in the column used for `ORDER BY`?

🧠 **Answer**: They can appear in any order (non-deterministic) unless you specify a **second column** for tie-breaking.

```sql
SELECT * FROM student ORDER BY dob;
```
If two students have the same DOB, you should add:
```sql
ORDER BY dob, id;
```

---

### Q2: How to fetch **top 3 highest paid** teachers from each department?

✅ Use `ROW_NUMBER()` or MySQL’s `LIMIT` with a subquery.

---

### Q3: Is `ORDER BY` before or after `LIMIT`?

🧠 **Answer**: `ORDER BY` is always before `LIMIT`.

```sql
SELECT * FROM teacher ORDER BY salary DESC LIMIT 5;
```

---

### Q4: Can you sort by a column that’s not in `SELECT`?

✅ Yes!

```sql
SELECT name FROM teacher ORDER BY salary DESC;
```

---

### Q5: Write a query to list all teachers with non-null salary in decreasing salary order, and if salaries are same, order by name ascending.

```sql
SELECT * FROM teacher
WHERE salary IS NOT NULL
ORDER BY salary DESC, name ASC;
```