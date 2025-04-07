

# 📊 SQL Aggregation Functions

Aggregation functions in SQL are used to **perform calculations on multiple rows** of a table's column and return a **single value**.

---

## ✅ Common Aggregate Functions

| Function | Description |
|----------|-------------|
| `COUNT()` | Returns the **number of rows** matching a condition |
| `SUM()`   | Returns the **total sum** of a numeric column |
| `AVG()`   | Returns the **average value** of a numeric column |
| `MIN()`   | Returns the **smallest value** in a column |
| `MAX()`   | Returns the **largest value** in a column |

---

## 🧪 Examples

Assume we have a `students` table:

```sql
SELECT * FROM students;
```

| id | name      | marks |
|----|-----------|-------|
| 1  | Aryan     | 88    |
| 2  | Neha      | 92    |
| 3  | Hitesh    | 76    |
| 4  | Manav     | 88    |
| 5  | Shreya    | NULL  |

---

### 🧮 COUNT

```sql
SELECT COUNT(*) FROM students;
-- Output: 5 (all rows, including NULLs)

SELECT COUNT(marks) FROM students;
-- Output: 4 (NULL is not counted)
```

---

### ➕ SUM

```sql
SELECT SUM(marks) FROM students;
-- Output: 344
```

---

### ⚖️ AVG

```sql
SELECT AVG(marks) FROM students;
-- Output: 86 (344 / 4)
```

---

### 📉 MIN and 📈 MAX

```sql
SELECT MIN(marks), MAX(marks) FROM students;
-- Output: MIN = 76, MAX = 92
```

---

## 🔎 With GROUP BY

```sql
SELECT dep_id, AVG(marks)
FROM students
GROUP BY dep_id;
```

This calculates the average marks **per department**.

---

## ❗ Common Interview Questions

1. **Q: What is the difference between `COUNT(*)` and `COUNT(column_name)`?**  
   A: `COUNT(*)` counts all rows; `COUNT(column_name)` skips rows with NULLs in that column.

2. **Q: What happens if all values are NULL in `SUM()` or `AVG()`?**  
   A: It returns `NULL`, not 0.

3. **Q: Can you use aggregation with `HAVING`?**  
   A: Yes! `HAVING` is used to filter aggregate results:
   ```sql
   SELECT dep_id, AVG(marks)
   FROM students
   GROUP BY dep_id
   HAVING AVG(marks) > 80;
   ```
