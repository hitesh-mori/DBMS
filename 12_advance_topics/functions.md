
---

## **📚 SQL Functions — Deep Dive**

### 1️⃣ What is a Function in SQL?

A **function** in SQL is a stored block of code that:

* Takes **parameters** (optional).
* Performs **some computation**.
* Returns a **single value** or a **table**.

💡 **Why use functions?**

* Code reusability.
* Cleaner queries.
* Centralized logic.
* Better maintainability.

---

## 2️⃣ Types of Functions

| Type                            | Returns                                   | Example                    |
| ------------------------------- | ----------------------------------------- | -------------------------- |
| **Scalar Function**             | Single value                              | `LEN(name)` returns length |
| **Table-Valued Function (TVF)** | Table result set                          | `GetTopEmployees()`        |
| **Aggregate Function**          | Single value from multiple rows           | `SUM(salary)`              |
| **Window Function**             | Value for each row considering other rows | `RANK()`                   |

---

## 3️⃣ Creating Functions — Syntax

### **MySQL:**

```sql
DELIMITER $$

CREATE FUNCTION FunctionName(param1 datatype, param2 datatype)
RETURNS return_datatype
DETERMINISTIC
BEGIN
    DECLARE result return_datatype;
    -- logic here
    RETURN result;
END$$

DELIMITER ;
```

---

### **PostgreSQL:**

```sql
CREATE OR REPLACE FUNCTION FunctionName(param1 datatype, param2 datatype)
RETURNS return_datatype AS $$
BEGIN
    -- logic here
    RETURN result;
END;
$$ LANGUAGE plpgsql;
```

---

### **SQL Server (T-SQL):**

```sql
CREATE FUNCTION dbo.FunctionName (@param1 datatype, @param2 datatype)
RETURNS return_datatype
AS
BEGIN
    DECLARE @result return_datatype;
    -- logic here
    RETURN @result;
END;
```

---

## 4️⃣ Examples of Different Functions

### **Example 1 — Scalar Function**

Return full name from first and last names.

```sql
CREATE FUNCTION GetFullName(first_name VARCHAR(50), last_name VARCHAR(50))
RETURNS VARCHAR(101)
DETERMINISTIC
BEGIN
    RETURN CONCAT(first_name, ' ', last_name);
END;
```

**Usage:**

```sql
SELECT GetFullName('John', 'Doe');
```

---

### **Example 2 — Scalar Function with Calculation**

Get yearly salary from monthly salary.

```sql
CREATE FUNCTION GetYearlySalary(monthly_salary DECIMAL(10,2))
RETURNS DECIMAL(12,2)
DETERMINISTIC
BEGIN
    RETURN monthly_salary * 12;
END;
```

---

### **Example 3 — Table-Valued Function**

Return employees with salary above a threshold.

```sql
CREATE FUNCTION GetHighEarners(min_salary DECIMAL(10,2))
RETURNS TABLE
RETURN (
    SELECT * FROM Employees WHERE salary > min_salary
);
```

**Usage:**

```sql
SELECT * FROM GetHighEarners(50000);
```

---

### **Example 4 — Function Calling Other Functions**

```sql
CREATE FUNCTION GetAnnualBonus(monthly_salary DECIMAL(10,2))
RETURNS DECIMAL(12,2)
BEGIN
    DECLARE yearly_salary DECIMAL(12,2);
    SET yearly_salary = GetYearlySalary(monthly_salary);
    RETURN yearly_salary * 0.1;
END;
```

---

### **Example 5 — Function with Conditional Logic**

```sql
CREATE FUNCTION GetPerformanceRating(score INT)
RETURNS VARCHAR(20)
BEGIN
    RETURN CASE
        WHEN score >= 90 THEN 'Excellent'
        WHEN score >= 75 THEN 'Good'
        ELSE 'Needs Improvement'
    END;
END;
```

---

## 5️⃣ Top 10 SQL Function Interview Questions

1. **Q:** Difference between `PROCEDURE` and `FUNCTION` in SQL?
   **A:**

   * **Function:** Must return a value, can be used in SELECT, cannot modify DB state (in most RDBMS).
   * **Procedure:** May or may not return a value, cannot be used in SELECT, can modify DB state.

2. **Q:** Can functions modify database data?
   **A:** In MySQL and SQL Server scalar functions generally cannot, but stored procedures can.

3. **Q:** Can a function call another function?
   **A:** Yes, nesting is allowed.

4. **Q:** Can we use transactions inside functions?
   **A:** Usually no (depends on DBMS) — functions should be deterministic.

5. **Q:** What’s the difference between deterministic and non-deterministic functions?
   **A:** Deterministic always returns same output for same input (`ABS()`), non-deterministic can change (`RAND()`).

6. **Q:** Can we return multiple values from a function?
   **A:** Not in scalar functions, but possible with table-valued functions.

7. **Q:** Can you pass table as parameter to a function?
   **A:** Yes in SQL Server (Table-Valued Parameters), no in MySQL directly.

8. **Q:** How to debug SQL functions?
   **A:** Use print statements in SQL Server (`PRINT`) or raise notices in PostgreSQL.

9. **Q:** Why avoid heavy logic in scalar functions in large queries?
   **A:** Performance issues — they execute row-by-row.

10. **Q:** Can we index a function’s output?
    **A:** Yes via computed/generated columns (depends on DBMS).

---

