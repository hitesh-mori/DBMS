

## 📘 What is an Outer Join?

An **Outer Join** in SQL returns records that have a match in both tables **as well as** records that **don’t have a match** in one of the tables. It is used to fetch complete information, including unmatched rows.

There are **three types** of outer joins:
- LEFT OUTER JOIN
- RIGHT OUTER JOIN
- FULL OUTER JOIN

---

## 🗂 Sample Tables

### 🎯 `employees` Table

| id | name     | dept_id |
|----|----------|---------|
| 1  | Alice    | 101     |
| 2  | Bob      | 102     |
| 3  | Charlie  | NULL    |
| 4  | David    | 104     |

### 🎯 `departments` Table

| id  | dept_name     |
|-----|---------------|
| 101 | HR            |
| 102 | Engineering   |
| 103 | Marketing     |

---

## 🔸 1. LEFT OUTER JOIN

### ✅ Description:
Returns **all rows from the left table** (`employees`) and matched rows from the right table (`departments`). If no match is found, NULLs are returned from the right table.

### 🧾 Query:
```sql
SELECT e.id, e.name, d.dept_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.id;
```

### 📤 Output:

| id | name    | dept_name   |
|----|---------|-------------|
| 1  | Alice   | HR          |
| 2  | Bob     | Engineering |
| 3  | Charlie | NULL        |
| 4  | David   | NULL        |

---

## 🔸 2. RIGHT OUTER JOIN

### ✅ Description:
Returns **all rows from the right table** (`departments`) and matched rows from the left table (`employees`). If no match is found, NULLs are returned from the left table.

### 🧾 Query:
```sql
SELECT e.id, e.name, d.dept_name
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.id;
```

### 📤 Output:

| id  | name  | dept_name   |
|-----|-------|-------------|
| 1   | Alice | HR          |
| 2   | Bob   | Engineering |
| NULL| NULL  | Marketing   |

---

## 🔸 3. FULL OUTER JOIN

### ✅ Description:
Returns **all rows from both tables**. Where there is a match, data is combined; otherwise, NULLs are shown for missing matches.

> Note: Not all databases (like MySQL) support FULL OUTER JOIN directly.

### 🧾 Query:
```sql
SELECT e.id, e.name, d.dept_name
FROM employees e
FULL OUTER JOIN departments d ON e.dept_id = d.id;
```

### 📤 Output:

| id  | name    | dept_name   |
|-----|---------|-------------|
| 1   | Alice   | HR          |
| 2   | Bob     | Engineering |
| 3   | Charlie | NULL        |
| 4   | David   | NULL        |
| NULL| NULL    | Marketing   |

---

## ⚠ Note:
- Use **`LEFT JOIN`** when you want all data from the left table.
- Use **`RIGHT JOIN`** when you want all data from the right table.
- Use **`FULL JOIN`** when you want to retain all rows from both tables.
- **FULL JOIN** is not supported in MySQL but can be simulated using `UNION`.

### 💡 Simulating FULL OUTER JOIN in MySQL:
```sql
SELECT e.id, e.name, d.dept_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.id

UNION

SELECT e.id, e.name, d.dept_name
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.id;
```

---

## 📚 Summary Table

| Join Type       | Returns                             |
|-----------------|--------------------------------------|
| LEFT OUTER JOIN | All rows from left + matched right  |
| RIGHT OUTER JOIN| All rows from right + matched left  |
| FULL OUTER JOIN | All rows from both tables           |

---

## 🧠 Tip
Use outer joins when:
- You need to identify **missing data**.
- You want to show records even when they **don’t have a match**.
- You’re preparing reports that require **comprehensive views** across tables.

---
