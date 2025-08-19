
# 🟢 Topic 7: Triggers in MySQL

### 🔹 What is a Trigger?

* A **Trigger** is a block of SQL code that executes **automatically** in response to certain events on a table.
* Events can be:

  * `INSERT`
  * `UPDATE`
  * `DELETE`

Think of triggers like **automatic reactions** to changes in the database.

---

## 🔹 Example Setup

We have two tables:

### `employees`

| emp\_id | name  | dept\_id | salary |
| ------- | ----- | -------- | ------ |
| 1       | Alice | 101      | 50000  |
| 2       | Bob   | 102      | 60000  |

### `employee_audit` (log table)

| action\_id | emp\_id | action | old\_salary | new\_salary | action\_time |
| ---------- | ------- | ------ | ----------- | ----------- | ------------ |

---

## 🔹 Example 1: Trigger BEFORE INSERT

We want to **make sure salary is never less than 30000** when inserting:

```sql
DELIMITER //

CREATE TRIGGER before_employee_insert
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    IF NEW.salary < 30000 THEN
        SET NEW.salary = 30000;
    END IF;
END //

DELIMITER ;
```

👉 Insert:

```sql
INSERT INTO employees (emp_id, name, dept_id, salary)
VALUES (3, 'Charlie', 101, 20000);
```

### Result (`employees` table):

| emp\_id                    | name    | dept\_id | salary |
| -------------------------- | ------- | -------- | ------ |
| 3                          | Charlie | 101      | 30000  |
| *(Salary auto-adjusted)* ✅ |         |          |        |

---

## 🔹 Example 2: Trigger AFTER UPDATE (Audit Log)

We want to log whenever salary changes:

```sql
DELIMITER //

CREATE TRIGGER after_employee_update
AFTER UPDATE ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_audit(emp_id, action, old_salary, new_salary, action_time)
    VALUES (OLD.emp_id, 'SALARY UPDATE', OLD.salary, NEW.salary, NOW());
END //

DELIMITER ;
```

👉 Update:

```sql
UPDATE employees
SET salary = 65000
WHERE emp_id = 2;
```

### `employee_audit` table:

| action\_id | emp\_id | action        | old\_salary | new\_salary | action\_time        |
| ---------- | ------- | ------------- | ----------- | ----------- | ------------------- |
| 1          | 2       | SALARY UPDATE | 60000       | 65000       | 2025-08-19 18:45:00 |

---

# 🔥 Top 10 Interview Questions on Triggers

1. **What is a Trigger in MySQL?**
   → An automatic action executed in response to INSERT, UPDATE, or DELETE.

2. **Difference between BEFORE and AFTER triggers?**
   → BEFORE → modify/validate data before insert/update.
   → AFTER → log/perform action after insert/update.

3. **Can we create a Trigger on SELECT?**
   → ❌ No, only on INSERT, UPDATE, DELETE.

4. **What is the difference between ROW-level and STATEMENT-level Triggers?**
   → In MySQL, triggers are always **row-level** (execute once for each row affected).

5. **What are NEW and OLD in Triggers?**
   → `NEW` → new value after insert/update.
   → `OLD` → previous value before update/delete.

6. **Can a Trigger call another Trigger?**
   → Indirectly yes, but MySQL prevents recursive trigger loops by default.

7. **What are practical use cases of Triggers?**
   → Audit logs, automatic data validation, history tables, enforcing constraints.

8. **Can Triggers modify other tables?**
   → ✅ Yes (common in audit logging).

9. **Difference between Trigger and Stored Procedure?**
   → Trigger runs automatically, Procedure must be called explicitly.

10. **Disadvantages of Triggers?**
    → Harder to debug, hidden logic, can impact performance if too many triggers run on large data changes.

---

✅ **Summary**:

* **Triggers = automation inside DB**.
* Use **BEFORE** to validate/change data, **AFTER** to log/audit.
* Controlled using `NEW` and `OLD` values.

---