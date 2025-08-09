

# 📘 SQL Subqueries – Complete Guide

## 🔍 What is a Subquery?

A **subquery** (also called an **inner query** or **nested query**) is a query **inside another query**.
The **outer query** uses the result of the subquery.

**Syntax:**

```sql
SELECT column_name
FROM table_name
WHERE column_name operator (SELECT ...);
```

---

## 🔹 Types of Subqueries

### **1. Scalar Subquery**

Returns **a single value** (one row, one column).

#### Example:

**Tables:**

**`employees`**

| id | name  | salary | dept\_id |
| -- | ----- | ------ | -------- |
| 1  | Alice | 5000   | 101      |
| 2  | Bob   | 7000   | 101      |
| 3  | Carol | 6000   | 102      |
| 4  | David | 5500   | 102      |

#### Query:

Find employees earning **more than the average salary**.

```sql
SELECT name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

#### Output:

| name | salary |
| ---- | ------ |
| Bob  | 7000   |

**💡 Note:** The subquery returns **a single number** → average salary.

---

### **2. Multi-row Subquery**

Returns **multiple rows** (one column, multiple rows).
Used with operators like `IN`, `ANY`, `ALL`.

#### Example:

Find employees working in departments where salary is **greater than 6000**.

```sql
SELECT name, salary
FROM employees
WHERE dept_id IN (
    SELECT dept_id
    FROM employees
    WHERE salary > 6000
);
```

#### Output:

| name  | salary |
| ----- | ------ |
| Alice | 5000   |
| Bob   | 7000   |

---

### **3. Correlated Subquery**

The inner query **depends on the outer query** for its value.
It runs **once for every row** in the outer query.

#### Example:

Find employees whose salary is **greater than the average salary of their department**.

```sql
SELECT name, salary, dept_id
FROM employees e1
WHERE salary > (
    SELECT AVG(salary)
    FROM employees e2
    WHERE e1.dept_id = e2.dept_id
);
```

#### Output:

| name  | salary | dept\_id |
| ----- | ------ | -------- |
| Bob   | 7000   | 101      |
| Carol | 6000   | 102      |

---

## 🔹 Inner Query vs Outer Query

* **Inner Query**: Runs first; result is passed to outer query.
* **Outer Query**: Uses result from inner query to filter, calculate, or join data.

---

## 📂 Example with All Types in One Table

**`departments`**

| dept\_id | dept\_name |
| -------- | ---------- |
| 101      | HR         |
| 102      | IT         |

**`employees`** *(as above)*

---

**Example 1 – Scalar:**

```sql
SELECT dept_name
FROM departments
WHERE dept_id = (SELECT dept_id FROM employees WHERE name = 'Bob');
```

**Example 2 – Multi-row:**

```sql
SELECT name
FROM employees
WHERE dept_id IN (SELECT dept_id FROM departments);
```

**Example 3 – Correlated:**

```sql
SELECT name
FROM employees e1
WHERE salary > (SELECT AVG(salary) FROM employees e2 WHERE e1.dept_id = e2.dept_id);
```

---

## ⚠ Common Mistakes:

1. Using scalar subquery when multiple rows are returned → **Error: subquery returns more than one row**.
2. Forgetting correlation in correlated subquery → gives wrong or unexpected results.
3. Performance issues if correlated subquery runs on large datasets without indexes.

---

## 🎯 Interview Questions & Answers

**Q1. Difference between subquery and join?**
**A:**

* **Subquery**: Query inside another query; used mainly in `WHERE`/`HAVING` clause.
* **Join**: Combines rows from two or more tables based on related columns.
* Subqueries are sometimes less efficient than joins.

**Q2. When to use a correlated subquery?**
**A:** When you need to compare each row to aggregated/calculated values from the same table.

**Q3. Can a subquery return more than one column?**
**A:** Yes, in the `FROM` clause (called **derived tables**), but not in `WHERE`/`HAVING`.

**Q4. Difference between `IN`, `ANY`, and `ALL` in multi-row subqueries?**
**A:**

* `IN`: Matches any value in the list.
* `ANY`: True if comparison is true for **at least one** value.
* `ALL`: True if comparison is true for **all** values.

**Q5. What is a scalar subquery and where is it used?**
**A:** Returns a single value; often used in `SELECT` list or conditions.

**Q6. How do you optimize a subquery?**
**A:** Use indexes, avoid correlated subqueries for large data, consider joins.

**Q7. Can subqueries be nested?**
**A:** Yes, you can have subqueries inside subqueries (multi-level nesting).

**Q8. Can we use subqueries in `FROM` clause?**
**A:** Yes, called **inline views** or **derived tables**.

**Q9. How does the execution order differ between subquery and correlated subquery?**
**A:**

* **Subquery**: Inner runs first, then outer.
* **Correlated**: Outer runs, then inner runs for each row.

**Q10. Can a subquery be used in an `UPDATE` or `DELETE` statement?**
**A:** Yes, for filtering rows based on another query's result.
