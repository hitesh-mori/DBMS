
# DML (Data Manipulation Language)

- DML commands are used to manipulate the data stored in the database.
- It is a subset of SQL commands used to **insert**, **update**, **delete**, and **retrieve** the data in a database.
- These commands **do not affect the schema** of the database (unlike DDL).
- DML operations **can be rolled back**, as they are not auto-committed by default.
- These commands are commonly used by general users or applications interacting with databases.

## 🔹 DML Commands

### 1. `INSERT`
- Used to insert new data into a table.
- Example:  
  ```sql
  INSERT INTO employees (id, name, department) VALUES (1, 'Alice', 'HR');
  ```

### 2. `UPDATE`
- Used to update existing records in a table.
- Example:  
  ```sql
  UPDATE employees SET department = 'Finance' WHERE id = 1;
  ```

### 3. `DELETE`
- Used to delete data from a table.
- Example:  
  ```sql
  DELETE FROM employees WHERE id = 1;
  ```
### 4. `CALL`

- Used to execute a stored procedure in the database.

- Helpful when business logic is encapsulated in procedures.

Example:
```sql
CALL increase_salary(1001, 5000);
```
---

### 🔁 Difference between DELETE and TRUNCATE (from DDL)

| Feature               | DELETE (DML)                        | TRUNCATE (DDL)                      |
|-----------------------|-------------------------------------|-------------------------------------|
| Command Type          | DML                                 | DDL                                 |
| Deletes               | Specific rows (with `WHERE`)        | All rows from the table             |
| Rollback              | Possible                            | Not possible (auto-committed)       |
| Triggers              | Fires triggers                      | Does not fire triggers              |
| Performance           | Slower (row-by-row delete)          | Faster (deallocates pages)          |
| Table Structure       | Remains intact                      | Remains intact                      |

---
