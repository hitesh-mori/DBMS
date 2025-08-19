

# 🟢 Topic 6: Stored Procedures & Functions

### 🔹 What are they?

* **Stored Procedure** → A set of SQL statements saved in the database and executed with a call.

  * Can have **IN, OUT, INOUT parameters**.
  * Good for **reusable business logic** (like inserting, updating, complex transactions).

* **Stored Function** → Similar, but **must return a single value**.

  * Good for **calculations** (like computing tax, age, discounts).


# 🔹 1. IN Parameter

* **Default type** if you don’t specify.
* Used to **pass input values** into the procedure.
* Value **cannot be modified** inside the procedure for the caller.

### Example:

```sql
DELIMITER //

CREATE PROCEDURE GetEmployeesByDept(IN dept INT)
BEGIN
    SELECT emp_id, name, salary
    FROM employees
    WHERE dept_id = dept;
END //

DELIMITER ;
```

👉 Call it:

```sql
CALL GetEmployeesByDept(101);
```

* Here `101` is passed **into** the procedure.
* Caller doesn’t get anything back directly (only result set).

---

# 🔹 2. OUT Parameter

* Used to **return values back to the caller**.
* Whatever is set inside procedure will be available outside.

### Example: return the **highest salary** in a department

```sql
DELIMITER //

CREATE PROCEDURE GetMaxSalaryByDept(
    IN dept INT,
    OUT maxSalary DECIMAL(10,2)
)
BEGIN
    SELECT MAX(salary) INTO maxSalary
    FROM employees
    WHERE dept_id = dept;
END //

DELIMITER ;
```

👉 Call it:

```sql
CALL GetMaxSalaryByDept(101, @result);
SELECT @result;
```

### Output:

```
@result = 55000
```

* `OUT` param gives result back via variable `@result`.

---

# 🔹 3. INOUT Parameter

* Acts as both **input and output**.
* You pass a value in, procedure can modify it, and return updated value.

### Example: increase salary by 10% and return it

```sql
DELIMITER //

CREATE PROCEDURE IncreaseSalary(
    INOUT empSalary DECIMAL(10,2)
)
BEGIN
    SET empSalary = empSalary * 1.10;
END //

DELIMITER ;
```

👉 Call it:

```sql
SET @sal = 50000;
CALL IncreaseSalary(@sal);
SELECT @sal;
```

### Output:

```
@sal = 55000
```

* Initially you pass `50000`.
* Procedure multiplies by `1.10`.
* Returns updated salary `55000`.

---

# 🔥 Quick Summary Table

| Parameter | Input Allowed? | Output Allowed? | Use Case                                        |
| --------- | -------------- | --------------- | ----------------------------------------------- |
| **IN**    | ✅ Yes          | ❌ No            | Pass data *into* procedure (default).           |
| **OUT**   | ❌ No           | ✅ Yes           | Return data *out* of procedure.                 |
| **INOUT** | ✅ Yes          | ✅ Yes           | Pass data in, modify, and return updated value. |


---

## 🔹 Example Setup

We’ll use the same **employees** table:

| emp\_id | name    | dept\_id | salary |
| ------- | ------- | -------- | ------ |
| 1       | Alice   | 101      | 50000  |
| 2       | Bob     | 102      | 60000  |
| 3       | Charlie | 101      | 55000  |
| 4       | David   | 103      | 70000  |

---

## 🔹 Stored Procedure Example

Let’s create a procedure that gives all employees in a department:

```sql
DELIMITER //

CREATE PROCEDURE GetEmployeesByDept(IN dept INT)
BEGIN
    SELECT emp_id, name, salary
    FROM employees
    WHERE dept_id = dept;
END //

DELIMITER ;
```

👉 Call it like this:

```sql
CALL GetEmployeesByDept(101);
```

### Output:

| emp\_id | name    | salary |
| ------- | ------- | ------ |
| 1       | Alice   | 50000  |
| 3       | Charlie | 55000  |

---

## 🔹 Stored Function Example

Let’s create a function to calculate yearly bonus (10% of salary):

```sql
DELIMITER //

CREATE FUNCTION CalculateBonus(empSalary DECIMAL(10,2))
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
    RETURN empSalary * 0.10;
END //

DELIMITER ;
```

👉 Use it inside a query:

```sql
SELECT name, salary, CalculateBonus(salary) AS bonus
FROM employees;
```

### Output:

| name    | salary | bonus |
| ------- | ------ | ----- |
| Alice   | 50000  | 5000  |
| Bob     | 60000  | 6000  |
| Charlie | 55000  | 5500  |
| David   | 70000  | 7000  |

---

# 🔥 Top 10 Interview Questions on Stored Procedures & Functions

1. **What is the difference between a Stored Procedure and a Function?**
   → Procedure may/may not return value, Function must return one.

2. **When would you use a Procedure vs a Function?**
   → Procedure → business logic, multiple statements, data modification.
   → Function → calculations, returning single values in SELECT.

3. **What are IN, OUT, and INOUT parameters in Procedures?**
   → IN: input only, OUT: output only, INOUT: both.

4. **Can Stored Procedures return multiple values?**
   → Yes, using OUT parameters.

5. **Can Stored Functions modify tables?**
   → No, Functions **cannot modify data** (INSERT/UPDATE/DELETE not allowed).

6. **Can a Procedure be used inside SELECT?**
   → No, only Functions can be used inside SELECT.

7. **What is the difference between Triggers and Procedures?**
   → Triggers run automatically on events; Procedures must be called explicitly.

8. **What are the advantages of Stored Procedures?**
   → Reusability, better security, reduced network traffic, encapsulated business logic.

9. **What are the disadvantages?**
   → Debugging difficulty, versioning complexity, execution overhead for very large logic.

10. **What is a Deterministic Function?**
    → A function that always returns the same result for the same input (important for replication).

---

✅ Summary:

* **Procedures** → Perform actions, can return multiple results, cannot be used in SELECT.
* **Functions** → Must return one value, can be used in SELECT, cannot change data.

