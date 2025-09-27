

# 💾 DML (Data Manipulation Language)

**Definition:**
DML commands are used to **manipulate the data stored in a database**. They allow users or applications to **insert, update, delete, and retrieve data** without affecting the database schema.

* **Subset of SQL:** Only affects data, not table structures (unlike DDL).
* **Transaction-safe:** Most DML operations can be rolled back if not auto-committed.
* **Used by:** Developers, applications, or general users to interact with data.

---

## 🔹 Common DML Commands

### **1. `INSERT`**

* **Purpose:** Adds new rows to a table.
* **Syntax:**

```sql
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);
```

* **Example:**

```sql
INSERT INTO employees (id, name, department, salary) 
VALUES (1, 'Alice', 'HR', 50000);
```

* **Notes:**

  * You can insert multiple rows in a single query:

```sql
INSERT INTO employees (id, name, department)
VALUES (2, 'Bob', 'Finance'),
       (3, 'Charlie', 'IT');
```

---

### **2. `UPDATE`**

* **Purpose:** Modifies existing records in a table.
* **Syntax:**

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

* **Example:**

```sql
UPDATE employees 
SET salary = 60000 
WHERE id = 1;
```

* **Notes:**

  * **Without `WHERE`**, all rows in the table will be updated.

---

### **3. `DELETE`**

* **Purpose:** Removes one or more rows from a table.
* **Syntax:**

```sql
DELETE FROM table_name
WHERE condition;
```

* **Example:**

```sql
DELETE FROM employees
WHERE id = 3;
```

* **Notes:**

  * **Without `WHERE`**, all rows will be deleted but table structure remains.
  * DML operation → can be rolled back if inside a transaction.

---

### **4. `SELECT`**

* **Purpose:** Retrieves data from one or more tables.
* **Syntax:**

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition
ORDER BY column1;
```

* **Example:**

```sql
SELECT name, department, salary 
FROM employees
WHERE salary > 50000
ORDER BY salary DESC;
```

* **Notes:**

  * `SELECT *` retrieves all columns.
  * Can include joins, grouping, filtering, and aggregation.

---

### **5. `CALL`**

* **Purpose:** Executes a **stored procedure** in the database.
* **Syntax:**

```sql
CALL procedure_name (param1, param2, ...);
```

* **Example:**

```sql
CALL increase_salary(1001, 5000);
```

* **Notes:**

  * Encapsulates business logic inside the database.
  * Can modify multiple tables or perform complex operations.

---

### **6. `MERGE` (Optional / Advanced DML)**

* **Purpose:** Combines **INSERT, UPDATE, DELETE** in a single operation based on condition (common in SQL Server / Oracle).
* **Syntax:**

```sql
MERGE INTO target_table AS t
USING source_table AS s
ON t.id = s.id
WHEN MATCHED THEN 
    UPDATE SET t.salary = s.salary
WHEN NOT MATCHED THEN 
    INSERT (id, salary) VALUES (s.id, s.salary);
```

* **Notes:**

  * Often used for **upserts** (insert if not exists, update if exists).

---

### **7. `LOCK TABLE` / `SELECT FOR UPDATE` (Optional DML-related)**

* **Purpose:** Ensures safe updates in transactions by locking rows/tables.
* Example:

```sql
SELECT * FROM employees WHERE id = 1 FOR UPDATE;
```

* **Notes:**

  * Prevents concurrent updates during a transaction.

---

## 🔁 **DELETE vs TRUNCATE**

| Feature              | DELETE (DML)                     | TRUNCATE (DDL)                                          |
| -------------------- | -------------------------------- | ------------------------------------------------------- |
| Command Type         | DML                              | DDL                                                     |
| Deletes              | Specific rows (can use `WHERE`)  | All rows from the table                                 |
| Rollback             | Possible (if inside transaction) | Usually not possible / auto-committed (depends on DBMS) |
| Triggers             | Fires triggers                   | Does not fire triggers                                  |
| Performance          | Slower (row-by-row)              | Faster (deallocates pages)                              |
| Table Structure      | Remains intact                   | Remains intact                                          |
| Auto-increment reset | No                               | Yes (resets to starting value)                          |

---


