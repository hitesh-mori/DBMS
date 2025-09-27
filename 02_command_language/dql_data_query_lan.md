
---

# 🔎 DQL (Data Query Language)

**Definition:**
DQL is a subset of SQL used to **query data from a database**.

* It is **read-only** — it only fetches data and **does not modify tables or data**.
* DQL operations are primarily based on the `SELECT` statement, which can include **filtering, sorting, aggregation, and joining** multiple tables.

---

## 🔹 DQL Command

### **1. `SELECT`**

The **primary DQL command** used to fetch data from one or more tables.

**Basic Syntax:**

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition
GROUP BY column
HAVING condition
ORDER BY column ASC|DESC;
```

---

### **2. Selecting Columns**

✅ Select all columns:

```sql
SELECT * FROM employees;
```

✅ Select specific columns:

```sql
SELECT name, department, salary FROM employees;
```

✅ Select distinct values:

```sql
SELECT DISTINCT department FROM employees;
```

---

### **3. Filtering Data (`WHERE` Clause)**

* Use conditions to filter rows:

```sql
SELECT * FROM employees
WHERE department = 'HR';
```

* Using logical operators:

```sql
SELECT * FROM employees
WHERE department = 'IT' AND salary > 50000;

SELECT * FROM employees
WHERE department = 'IT' OR department = 'HR';

SELECT * FROM employees
WHERE salary BETWEEN 30000 AND 60000;

SELECT * FROM employees
WHERE name LIKE 'A%';  -- Names starting with 'A'
```

---

### **4. Sorting Data (`ORDER BY`)**

```sql
SELECT * FROM employees
ORDER BY salary DESC;  -- Descending
```

* Multiple columns:

```sql
SELECT * FROM employees
ORDER BY department ASC, salary DESC;
```

---

### **5. Aggregation (`GROUP BY`)**

* Summarize data with aggregate functions:

```sql
SELECT department, COUNT(*) AS num_employees
FROM employees
GROUP BY department;
```

* Other aggregate functions:

```sql
SELECT department, SUM(salary) AS total_salary,
       AVG(salary) AS avg_salary,
       MIN(salary) AS min_salary,
       MAX(salary) AS max_salary
FROM employees
GROUP BY department;
```

* Filtering grouped data with `HAVING`:

```sql
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

---

### **6. Joining Tables (`JOIN`)**

* Combine data from multiple tables:

**Inner Join (matching rows only):**

```sql
SELECT e.name, d.department_name
FROM employees e
INNER JOIN departments d
ON e.department_id = d.id;
```

**Left Join (all from left, matching from right):**

```sql
SELECT e.name, d.department_name
FROM employees e
LEFT JOIN departments d
ON e.department_id = d.id;
```

**Right Join (all from right, matching from left):**

```sql
SELECT e.name, d.department_name
FROM employees e
RIGHT JOIN departments d
ON e.department_id = d.id;
```

**Full Outer Join (all rows from both tables, unmatched NULLs):**

```sql
SELECT e.name, d.department_name
FROM employees e
FULL OUTER JOIN departments d
ON e.department_id = d.id;
```

---

### **7. Subqueries / Nested Queries**

* Using a query inside another:

```sql
-- Employees with salary higher than average
SELECT name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

* In `FROM` clause:

```sql
SELECT dept, MAX(salary)
FROM (SELECT department AS dept, salary FROM employees) AS sub
GROUP BY dept;
```

---

### **8. Limiting Results (`LIMIT` / `TOP`)**

* MySQL / PostgreSQL:

```sql
SELECT * FROM employees
ORDER BY salary DESC
LIMIT 5;
```

* SQL Server:

```sql
SELECT TOP 5 * FROM employees
ORDER BY salary DESC;
```

---

### **9. Set Operations**

* Combine results of multiple SELECT queries:

```sql
-- UNION (distinct values)
SELECT department FROM employees
UNION
SELECT department FROM contractors;

-- UNION ALL (including duplicates)
SELECT department FROM employees
UNION ALL
SELECT department FROM contractors;
```

* INTERSECT (common rows):

```sql
SELECT department FROM employees
INTERSECT
SELECT department FROM contractors;
```

* EXCEPT / MINUS (rows in first query but not in second):

```sql
SELECT department FROM employees
EXCEPT
SELECT department FROM contractors;
```

---

### **10. Aliases**

* Rename columns or tables in query results:

```sql
SELECT name AS employee_name, salary AS emp_salary
FROM employees e;

SELECT e.name, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.id;
```

---

## 📝 Notes

1. DQL is **read-only**; it does **not modify** data or table structure.
2. Clauses often used with DQL: `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY`, `JOIN`, `LIMIT`.
3. Useful for **reporting, analytics, dashboards**, and extracting insights.
4. Subqueries, joins, and aggregation make DQL very powerful for complex queries.

---

