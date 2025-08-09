
# 📘 **SELF JOIN in SQL**

A **SELF JOIN** is when a table is joined **with itself**.
It’s useful for situations where **rows in a table are related to other rows in the same table**.
We typically **alias** the same table with different names (e.g., `e1`, `e2`) to differentiate the two instances.

---

## 🗂 Sample Table – `employee`

| id  | name   | salary | dob        | manager\_id |
| --- | ------ | ------ | ---------- | ----------- |
| 101 | Jack   | 2000   | 1997-05-19 | 104         |
| 102 | Clark  | NULL   | NULL       | 109         |
| 103 | Mack   | 6000   | 1997-03-10 | 101         |
| 104 | Peter  | 4000   | 1998-07-16 | NULL        |
| 105 | Tom    | 3000   | 1998-11-03 | 109         |
| 106 | Leo    | 2500   | 1997-10-10 | 110         |
| 107 | Roger  | 5300   | 1997-06-17 | NULL        |
| 108 | Mike   | 2000   | 1998-03-09 | 105         |
| 109 | Paul   | 4800   | 1998-12-28 | 105         |
| 110 | Hannah | 2000   | 1999-09-26 | 103         |

---

## 🔹 1. **Basic SELF JOIN Example**

Retrieve each employee’s details along with their manager’s name.

```sql
SELECT 
    e1.id AS emp_id,
    e1.name AS emp_name,
    e1.salary,
    e2.name AS manager_name
FROM employee e1
LEFT JOIN employee e2
    ON e1.manager_id = e2.id;
```

### 📤 Output:

| emp\_id | emp\_name | salary | manager\_name |
| ------- | --------- | ------ | ------------- |
| 101     | Jack      | 2000   | Peter         |
| 102     | Clark     | NULL   | Paul          |
| 103     | Mack      | 6000   | Jack          |
| 104     | Peter     | 4000   | NULL          |
| 105     | Tom       | 3000   | Paul          |
| 106     | Leo       | 2500   | Hannah        |
| 107     | Roger     | 5300   | NULL          |
| 108     | Mike      | 2000   | Tom           |
| 109     | Paul      | 4800   | Tom           |
| 110     | Hannah    | 2000   | Mack          |

> **Note:** We used `LEFT JOIN` to include employees **without managers**.

---

## 🔹 2. **Filtering Only Employees with Managers**

```sql
SELECT 
    e1.id AS emp_id,
    e1.name AS emp_name,
    e1.salary,
    e2.name AS manager_name
FROM employee e1
INNER JOIN employee e2
    ON e1.manager_id = e2.id;
```

This **removes** rows where `manager_id` is NULL.

---

## 🔹 3. **SELF JOIN with Additional Conditions**

Find employees whose manager’s salary is **greater than** their own.

```sql
SELECT 
    e1.name AS emp_name,
    e1.salary AS emp_salary,
    e2.name AS manager_name,
    e2.salary AS manager_salary
FROM employee e1
JOIN employee e2
    ON e1.manager_id = e2.id
WHERE e2.salary > e1.salary;
```

---

## 🔹 4. **SELF JOIN with GROUP BY + HAVING**

Count how many employees each manager has, **only showing managers with more than 1 employee**.

```sql
SELECT 
    e2.name AS manager_name,
    COUNT(e1.id) AS num_employees
FROM employee e1
JOIN employee e2
    ON e1.manager_id = e2.id
GROUP BY e2.name
HAVING COUNT(e1.id) > 1;
```

---

## 📚 **When to Use SELF JOIN**

* Finding **managers and subordinates**
* **Hierarchy** structures (e.g., org charts)
* Comparing rows in the **same table**
* Recursive relationships

---

## 🎯 **Top 10 SELF JOIN Interview Questions with Answers**

| #  | Question                                                            | Answer                                                                        |
| -- | ------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| 1  | What is a SELF JOIN?                                                | A join where a table is joined with itself.                                   |
| 2  | Why do we alias tables in SELF JOIN?                                | To differentiate between the two instances of the same table.                 |
| 3  | What’s the difference between INNER and LEFT SELF JOIN?             | INNER excludes rows with no match; LEFT includes them with NULLs.             |
| 4  | Can SELF JOIN be used with more than 2 instances of the same table? | Yes, but each needs its own alias.                                            |
| 5  | Example use case of SELF JOIN?                                      | Finding employees and their managers from one employee table.                 |
| 6  | Performance concern in SELF JOIN?                                   | Can be expensive on large tables due to matching each row against all others. |
| 7  | Can we apply WHERE in SELF JOIN?                                    | Yes, to filter based on relationships or attributes.                          |
| 8  | Is SELF JOIN the same as CROSS JOIN?                                | No. CROSS JOIN returns Cartesian product; SELF JOIN uses a condition.         |
| 9  | Can we use SELF JOIN for hierarchical data?                         | Yes, it’s often used to navigate parent-child relationships.                  |
| 10 | What if `manager_id` points to an ID that doesn’t exist?            | That row will have NULL in manager columns with LEFT JOIN.                    |

