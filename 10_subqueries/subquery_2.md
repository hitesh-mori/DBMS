
## 1️⃣ Sample Table Setup

```sql
CREATE TABLE employees (
    emp_id INT,
    name VARCHAR(50),
    dept_id INT,
    salary INT
);

INSERT INTO employees VALUES
(1, 'John', 10, 5000),
(2, 'Alice', 20, 7000),
(3, 'Bob', 10, 8000),
(4, 'David', 30, 6000),
(5, 'Emma', 20, 9000);

CREATE TABLE departments (
    dept_id INT,
    dept_name VARCHAR(50)
);

INSERT INTO departments VALUES
(10, 'HR'),
(20, 'IT'),
(30, 'Finance'),
(40, 'Admin');
```

---

## 2️⃣ `IN` Operator

Find employees in departments where salary > 8000:

```sql
SELECT name, dept_id
FROM employees
WHERE dept_id IN (
    SELECT dept_id
    FROM employees
    WHERE salary > 8000
);
```

**Output**

| name  | dept\_id |
| ----- | -------- |
| Alice | 20       |
| Emma  | 20       |

💡 **Note:** Subquery must return **1 column**.

---

## 3️⃣ `ANY` Operator

`ANY` → condition must be true for **at least one** value.

```sql
SELECT name, salary
FROM employees
WHERE salary > ANY (
    SELECT salary
    FROM employees
    WHERE dept_id = 10
);
```

**Explanation**: Salaries in dept\_id=10 are `{5000, 8000}` → `> ANY` means greater than **at least one** (so greater than 5000).
**Output**

| name  | salary |
| ----- | ------ |
| Alice | 7000   |
| Bob   | 8000   |
| David | 6000   |
| Emma  | 9000   |

---

## 4️⃣ `ALL` Operator

`ALL` → condition must be true for **every** value.

```sql
SELECT name, salary
FROM employees
WHERE salary > ALL (
    SELECT salary
    FROM employees
    WHERE dept_id = 10
);
```

**Explanation**: Salaries in dept\_id=10 are `{5000, 8000}` → `> ALL` means greater than **both 5000 and 8000** → greater than 8000.
**Output**

| name | salary |
| ---- | ------ |
| Emma | 9000   |

---

## 5️⃣ `EXISTS` Operator

`EXISTS` → checks if **subquery returns at least one row**.

```sql
SELECT name, dept_id
FROM employees e
WHERE EXISTS (
    SELECT 1
    FROM departments d
    WHERE d.dept_id = e.dept_id
);
```

**Output**

| name  | dept\_id |
| ----- | -------- |
| John  | 10       |
| Alice | 20       |
| Bob   | 10       |
| David | 30       |
| Emma  | 20       |

💡 **Note:** If the subquery finds even one matching dept, the row is included.

---

## 6️⃣ `EXISTS` vs `IN` vs `JOIN`

| Feature                | `EXISTS`                             | `IN`                                   | `JOIN`                             |
| ---------------------- | ------------------------------------ | -------------------------------------- | ---------------------------------- |
| Returns                | True/False per row (boolean check)   | Matches column values in a list        | Combines rows from multiple tables |
| Speed (large datasets) | Often faster with correlated queries | Slower if subquery returns many rows   | Usually fastest for retrieval      |
| Use case               | Check **if any match exists**        | Match against a list of values         | Retrieve combined data             |
| Columns needed         | Subquery can have `SELECT 1`         | Must match value type and column count | No restriction on columns          |

---

## 7️⃣ **Top 10 Interview Questions & Answers**

### Q1: Difference between `EXISTS` and `IN`?

**A:**

* `IN` → compares a value with a **list** from subquery.
* `EXISTS` → checks if **subquery returns rows**.
* `EXISTS` stops searching after finding the first match; `IN` retrieves the full list before comparing.

---

### Q2: Difference between `ANY` and `ALL`?

**A:**

* `ANY` → condition true for at least one value in subquery.
* `ALL` → condition true for all values in subquery.

---

### Q3: Can `IN` subquery have multiple columns?

**A:** Yes, but only with tuple comparison:

```sql
WHERE (col1, col2) IN (SELECT col1, col2 FROM table);
```

---

### Q4: Which is faster — `EXISTS` or `IN`?

**A:**

* `EXISTS` is usually faster when subquery returns large result sets.
* `IN` can be faster when subquery returns a small static list.

---

### Q5: Can `EXISTS` return columns from subquery?

**A:** No. It only returns **TRUE/FALSE**; you can only retrieve columns from outer query.

---

### Q6: When to use `JOIN` instead of `IN`?

**A:** Use `JOIN` when you need columns from both tables, not just filtering.

---

### Q7: What is a correlated subquery?

**A:** A subquery that uses columns from the outer query inside it — runs once per outer row.

---

### Q8: Can we use `EXISTS` without `SELECT *`?

**A:** Yes. Common pattern is `SELECT 1` or `SELECT NULL` because we don’t care about columns.

---

### Q9: How is `= ANY` different from `IN`?

**A:** `col = ANY(subquery)` is equivalent to `col IN (subquery)`, but `ANY` can also be used with `<`, `>`, `<=`, etc.

---

### Q10: Can `ALL` work with `<` operator?

**A:** Yes. Example:

```sql
salary < ALL (SELECT salary FROM employees WHERE dept_id = 20);
```

Finds salaries less than **every** salary in dept 20.

