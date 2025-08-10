


# SQL Ranking Functions

## **Definition of RANK in SQL**
`RANK()` is a **window function** in SQL that assigns a **ranking number** to each row within a result set based on the **order** specified in the `ORDER BY` clause. Rows with **equal values** in the ordering column(s) receive the **same rank**, and the next rank is **skipped** according to the number of tied rows.

### Example:
If salaries are sorted in descending order:

| Salary | RANK() |
| ------ | ------ |
| 6000   | 1      |
| 6000   | 1      |
| 5000   | 3      |
| 4000   | 4      |

---

## **📌 Part 1 — 5 Different Queries using RANK()**

### 1️⃣ Basic ranking by salary
```sql
SELECT 
    employee_id,
    name,
    salary,
    RANK() OVER (ORDER BY salary DESC) AS rank_no
FROM employees;
````

Highest salary gets rank 1; ties share the same rank; numbers get skipped.

---

### 2️⃣ Ranking within a department (Partitioning)

```sql
SELECT 
    employee_id,
    name,
    department_id,
    salary,
    RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS dept_rank
FROM employees;
```

Resets ranking **per department**.

---

### 3️⃣ Ranking by joining two tables

```sql
SELECT 
    e.employee_id,
    e.name,
    d.department_name,
    e.salary,
    RANK() OVER (PARTITION BY d.department_name ORDER BY e.salary DESC) AS dept_rank
FROM employees e
JOIN departments d ON e.department_id = d.department_id;
```

Ranks within each department name after joining.

---

### 4️⃣ Ranking with a subquery

```sql
SELECT *
FROM (
    SELECT 
        employee_id,
        name,
        salary,
        RANK() OVER (ORDER BY salary DESC) AS rank_no
    FROM employees
) ranked
WHERE rank_no <= 3;
```

Finds **top 3 salaries**.

---

### 5️⃣ Finding the 2nd highest salary using RANK()

```sql
SELECT salary
FROM (
    SELECT salary, RANK() OVER (ORDER BY salary DESC) AS rnk
    FROM employees
) ranked
WHERE rnk = 2;
```

Easily finds N-th highest value.

---

## **📌 Part 2 — Example with TWO Tables + Subquery**

### Tables:

**employees**
\| emp\_id | name | dept\_id | salary |

**departments**
\| dept\_id | dept\_name |

### Query: Top 2 salaries per department

```sql
SELECT *
FROM (
    SELECT 
        e.emp_id,
        e.name,
        d.dept_name,
        e.salary,
        RANK() OVER (PARTITION BY d.dept_name ORDER BY e.salary DESC) AS dept_rank
    FROM employees e
    JOIN departments d ON e.dept_id = d.dept_id
) ranked
WHERE dept_rank <= 2;
```

---

# SQL Ranking Functions — Types

Ranking functions are **window functions** that assign a numeric position to each row based on a specified order. They are often used for **ranking, top-N queries, leaderboards, and analytics**.

---

## 1. `RANK()`

Assigns a rank to each row; ties get same rank; next rank skips numbers.

```sql
RANK() OVER (ORDER BY column DESC)
```

Example:

| Salary | RANK() |
| ------ | ------ |
| 6000   | 1      |
| 6000   | 1      |
| 5000   | 3      |
| 4000   | 4      |

---

## 2. `DENSE_RANK()`

Similar to `RANK()`, but no skipped numbers after ties.

```sql
DENSE_RANK() OVER (ORDER BY column DESC)
```

Example:

| Salary | DENSE\_RANK() |
| ------ | ------------- |
| 6000   | 1             |
| 6000   | 1             |
| 5000   | 2             |
| 4000   | 3             |

---

## 3. `ROW_NUMBER()`

Assigns a unique sequential number to each row.

```sql
ROW_NUMBER() OVER (ORDER BY column DESC)
```

Example:

| Salary | ROW\_NUMBER() |
| ------ | ------------- |
| 6000   | 1             |
| 6000   | 2             |
| 5000   | 3             |
| 4000   | 4             |

---

## 4. `NTILE(n)`

Divides result set into n equal groups, assigning a bucket number.

```sql
NTILE(4) OVER (ORDER BY column DESC)
```

Example with `NTILE(2)`:

| Salary | NTILE(2) |
| ------ | -------- |
| 6000   | 1        |
| 6000   | 1        |
| 5000   | 2        |
| 4000   | 2        |

---

## Summary Table

| Function    | Ties Allowed | Skips Rank After Ties? | Unique Numbers | Groups Rows? |
| ----------- | ------------ | ---------------------- | -------------- | ------------ |
| RANK        | ✅            | ✅                      | ❌              | ❌            |
| DENSE\_RANK | ✅            | ❌                      | ❌              | ❌            |
| ROW\_NUMBER | ❌            | ❌                      | ✅              | ❌            |
| NTILE       | ✅            | N/A                    | ❌              | ✅            |

---

## **📌 Part 3 — Top 10 Interview Questions & Answers on RANK()**

**Q1:** Difference between `RANK()`, `DENSE_RANK()`, and `ROW_NUMBER()`?
**A:** `RANK()` → Ties share rank, skips numbers; `DENSE_RANK()` → Ties share rank, no skips; `ROW_NUMBER()` → Unique numbers for all rows.

---

**Q2:** How do you get the N-th highest salary using `RANK()`?

```sql
SELECT salary
FROM (
    SELECT salary, RANK() OVER (ORDER BY salary DESC) AS rnk
    FROM employees
) ranked
WHERE rnk = N;
```

---

**Q3:** How to reset ranking for each group?
**A:** Use `PARTITION BY`:

```sql
RANK() OVER (PARTITION BY department_id ORDER BY salary DESC)
```

---

**Q4:** Can you use `RANK()` in `WHERE` clause directly?
**A:** No — must wrap in subquery or CTE.

---

**Q5:** How does SQL calculate `RANK()`?
**A:** Sorts data, assigns rank 1 to first row, ties share rank, skips based on number of ties.

---

**Q6:** When use `RANK()` instead of `DENSE_RANK()`?
**A:** Use `RANK()` for competition ranking where ties skip numbers.

---

**Q7:** Can `RANK()` work without `ORDER BY`?
**A:** Yes, but order is undefined and results meaningless.

---

**Q8:** How to get top N per group using `RANK()`?

```sql
SELECT *
FROM (
    SELECT emp_id, dept_id, salary,
           RANK() OVER (PARTITION BY dept_id ORDER BY salary DESC) AS rnk
    FROM employees
) t
WHERE rnk <= N;
```

---

**Q9:** Does `RANK()` improve performance over `GROUP BY`?
**A:** No — they serve different purposes; `GROUP BY` aggregates, `RANK()` assigns rankings.

---

**Q10:** Is `RANK()` deterministic?
**A:** Only if `ORDER BY` specifies a unique order; otherwise ties may be ordered arbitrarily.

```

---

If you want, I can also add **visual diagrams** showing how ranks are assigned for each type — that makes it even easier to memorize for interviews.
```
