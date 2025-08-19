
# 🟢 Topic 5: **Views in MySQL**

### 🔹 What is a View?

A **view** is a **virtual table** created from the result of a query.

* It doesn’t store data itself.
* It just “remembers” a query and behaves like a table.
* Useful for **simplifying complex queries** or **restricting access** to certain columns.

---

## 🔹 Example Setup (Tables)

Let’s say we have two tables:

### `employees`

| emp\_id | name    | dept\_id | salary |
| ------- | ------- | -------- | ------ |
| 1       | Alice   | 101      | 50000  |
| 2       | Bob     | 102      | 60000  |
| 3       | Charlie | 101      | 55000  |
| 4       | David   | 103      | 70000  |

### `departments`

| dept\_id | dept\_name |
| -------- | ---------- |
| 101      | HR         |
| 102      | IT         |
| 103      | Marketing  |

---

## 🔹 Creating a View

Suppose we often want to see employee details along with their department name.
Instead of writing a `JOIN` every time, we can make a **view**:

```sql
CREATE VIEW emp_dept_view AS
SELECT e.emp_id, e.name, d.dept_name, e.salary
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id;
```

---

## 🔹 Using the View

```sql
SELECT * FROM emp_dept_view;
```

### Output:

| emp\_id | name    | dept\_name | salary |
| ------- | ------- | ---------- | ------ |
| 1       | Alice   | HR         | 50000  |
| 2       | Bob     | IT         | 60000  |
| 3       | Charlie | HR         | 55000  |
| 4       | David   | Marketing  | 70000  |

---

## 🔹 Updating Data through Views

If the view is **updatable** (simple SELECT, no aggregations), you can insert/update:

```sql
UPDATE emp_dept_view
SET salary = 80000
WHERE name = 'David';
```

This will update the `employees` table as well.

---

## 🔹 Dropping a View

```sql
DROP VIEW emp_dept_view;
```

---

# 🔥 Top 10 Interview Questions on Views

1. **What is a View in MySQL and why is it used?**
   → A virtual table based on a query, used for simplifying queries, security, and abstraction.

2. **Difference between a View and a Table?**
   → Table stores data; view stores only query definition.

3. **Can we update a View?**
   → Yes, if it is based on a single table and doesn’t use aggregations, DISTINCT, GROUP BY, etc.

4. **What are the advantages of using Views?**
   → Security (hide sensitive columns), query simplification, data abstraction.

5. **What are the limitations of Views?**
   → Cannot have indexes, performance overhead if query is complex, some views are not updatable.

6. **What is a Materialized View? Does MySQL support it?**
   → A materialized view stores query results physically (like a cached table).
   MySQL **does not natively support materialized views**.

7. **Can we join multiple tables inside a View?**
   → Yes, views can contain joins.

8. **What happens if the underlying table is dropped?**
   → The view becomes invalid.

9. **Can a View call another View?**
   → Yes, a view can be created from another view.

10. **How do Views affect performance?**
    → Views don’t inherently improve performance; they just simplify queries.
    If the view query is complex, it may slow things down.

