

## 🔍 WHERE Clause — **What and Where?**

### ✅ Purpose:
The `WHERE` clause is used to **filter rows** — only return rows that match a condition.

---

## 🧠 Rule:
The `WHERE` clause comes **after `FROM` or `JOIN`**, and **before** `GROUP BY`, `ORDER BY`, or `LIMIT`.

---

### ✅ Basic Syntax:

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

---

### ✅ With JOIN:

```sql
SELECT e.name, d.department_name
FROM employees e
JOIN departments d ON e.dep_id = d.id
WHERE d.location = 'New York';
```

---

### ✅ With GROUP BY and ORDER BY:

```sql
SELECT department, COUNT(*) AS num_employees
FROM employees
WHERE salary > 50000
GROUP BY department
ORDER BY num_employees DESC;
```

---

## ❌ Incorrect Usage:

```sql
-- ❌ Wrong: WHERE before FROM
SELECT name
WHERE salary > 50000
FROM employees;

-- ❌ Wrong: WHERE after ORDER BY
SELECT name
FROM employees
ORDER BY salary
WHERE salary > 50000;
```

---

## ✅ Correct Order of Clauses in SQL:

```
SELECT        -- what you want to see
FROM          -- where the data comes from
JOIN          -- how to combine tables
WHERE         -- filter rows
GROUP BY      -- group rows
HAVING        -- filter groups
ORDER BY      -- sort results
LIMIT         -- restrict number of rows
```