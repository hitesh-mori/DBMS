

# 📘 SQL `GROUP BY` – Complete Guide

The `GROUP BY` clause in SQL is used to group rows that have the same values in specified columns into **summary rows** (like "total salary per department").

---

## 🔹 Syntax

```sql
SELECT column_name, AGGREGATE_FUNCTION(column_name)
FROM table_name
WHERE condition
GROUP BY column_name;
```

---

## ✅ 1. GROUP BY Single Column

```sql
SELECT dep_id, COUNT(*) AS total_students
FROM students
GROUP BY dep_id;
```

📌 Groups all students by their department.

---

## ✅ 2. GROUP BY Multiple Columns

```sql
SELECT dep_id, gender, COUNT(*) AS total_students
FROM students
GROUP BY dep_id, gender;
```

📌 Groups by department and gender — gives count of male/female in each department.

---

## ✅ 3. GROUP BY with WHERE Clause

```sql
SELECT dep_id, AVG(marks) AS avg_marks
FROM students
WHERE marks IS NOT NULL
GROUP BY dep_id;
```

📌 First filters rows, then groups. `WHERE` always comes before `GROUP BY`.

---

## ✅ 4. GROUP BY with ORDER BY

```sql
SELECT dep_id, COUNT(*) AS total_students
FROM students
GROUP BY dep_id
ORDER BY total_students DESC;
```

📌 Sorts grouped results based on the aggregate value.

---

## ✅ 5. GROUP BY with Aggregate Functions

Common use with:

- `COUNT()`
- `SUM()`
- `AVG()`
- `MAX()`
- `MIN()`

```sql
SELECT dep_id, AVG(marks) AS avg_marks, MAX(marks) AS top_score
FROM students
GROUP BY dep_id;
```

📌 Gives average and top score per department.

---

## ✅ 6. GROUP BY with HAVING Clause

```sql
SELECT dep_id, AVG(marks) AS avg_marks
FROM students
GROUP BY dep_id
HAVING AVG(marks) > 75;
```

📌 `HAVING` is like `WHERE` but for **aggregated data**.

---

## 🧠 INTERVIEW QUESTIONS & ANSWERS

---

### Q1: What’s the difference between `WHERE` and `HAVING`?

👉 `WHERE` filters **rows before** grouping, `HAVING` filters **groups after** aggregation.

---

### Q2: Can we use `GROUP BY` without aggregate functions?

✅ Yes, but it's rare:
```sql
SELECT dep_id FROM students GROUP BY dep_id;
```

---

### Q3: What will happen if we select a column that is not in `GROUP BY` or inside an aggregate?

❌ MySQL may allow it (depending on SQL mode), but **standard SQL throws an error**. Always use only grouped columns or aggregates in `SELECT`.

---

### Q4: Difference between `GROUP BY` and `PARTITION BY`?

- `GROUP BY` → summarizes rows into one result per group.
- `PARTITION BY` (used in window functions) → keeps all rows, just divides them logically.

---

### Q5: Can we group by aliases?

✅ Yes, but only in `ORDER BY`, **not** in `GROUP BY`.
Aliases not worked in where clause
```sql
SELECT dep_id AS dept FROM students GROUP BY dept; -- ❌
SELECT dep_id AS dept FROM students GROUP BY dep_id; -- ✅
```

---

### Q6: How to get top 1 scorer per department?

```sql
SELECT dep_id, MAX(marks) AS top_score
FROM students
GROUP BY dep_id;
```

---

### Q7: Get departments having more than 5 students and average marks > 80?

```sql
SELECT dep_id, COUNT(*) AS cnt, AVG(marks) AS avg_marks
FROM students
GROUP BY dep_id
HAVING cnt > 5 AND avg_marks > 80;
```
