
# 📚 Data Definition Language (DDL)

## What is DDL?

**DDL (Data Definition Language)** consists of SQL commands used to define, modify, and delete the *structure* of database objects such as tables, views, schemas, etc. It does **not manipulate data** directly.

### 📝 Key Characteristics:
- Defines the **database schema**.
- Commands include `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, etc.
- These commands are **auto-committed** (changes are immediately saved and cannot be rolled back).
- Usually not used by general users directly; used during development or setup.

---

## 🔧 Common DDL Commands:

### 1. `CREATE`
Used to **create** a new database or database objects like:
- Tables
- Indexes
- Views
- Stored procedures
- Triggers
- Functions

**Example:**
```sql
CREATE TABLE employees (
  id INT PRIMARY KEY,
  name VARCHAR(100),
  salary FLOAT
);

```

## 2. `ALTER`

Used to **modify the structure** of existing database objects, especially tables.

---

### **1. Add a Column**

```sql
ALTER TABLE employees 
ADD age INT;
```

---

### **2. Drop a Column**

```sql
ALTER TABLE employees
DROP COLUMN age;
```

---

### **3. Rename a Column**

```sql
-- MySQL / PostgreSQL / Oracle
ALTER TABLE employees
RENAME COLUMN id TO employee_id;

-- SQL Server
EXEC sp_rename 'employees.id', 'employee_id', 'COLUMN';
```

---

### **4. Rename a Table**

```sql
-- MySQL / PostgreSQL / Oracle
ALTER TABLE old_table_name
RENAME TO new_table_name;

-- SQL Server
EXEC sp_rename 'old_table_name', 'new_table_name';
```

---

### **5. Modify Column Data Type**

```sql
-- MySQL
ALTER TABLE employees
MODIFY salary DECIMAL(10,2);

-- SQL Server
ALTER TABLE employees
ALTER COLUMN salary DECIMAL(10,2);

-- PostgreSQL
ALTER TABLE employees
ALTER COLUMN salary TYPE NUMERIC(10,2);

-- Oracle
ALTER TABLE employees
MODIFY (salary NUMBER(10,2));
```

---

### **6. Set / Drop NOT NULL**

```sql
-- Set NOT NULL
ALTER TABLE employees
MODIFY age INT NOT NULL;

-- Drop NOT NULL
ALTER TABLE employees
MODIFY age INT NULL;
```

> Note: SQL Server uses `ALTER COLUMN` instead of `MODIFY`.

---

### **7. Add a Constraint**

```sql
-- Add PRIMARY KEY
ALTER TABLE employees
ADD CONSTRAINT pk_emp_id PRIMARY KEY (employee_id);

-- Add FOREIGN KEY
ALTER TABLE orders
ADD CONSTRAINT fk_customer_id
FOREIGN KEY (customer_id) REFERENCES customers(id);

-- Add UNIQUE
ALTER TABLE employees
ADD CONSTRAINT uq_email UNIQUE (email);

-- Add CHECK
ALTER TABLE employees
ADD CONSTRAINT chk_salary CHECK (salary > 0);
```

---

### **8. Drop a Constraint**

```sql
-- Generic
ALTER TABLE employees
DROP CONSTRAINT constraint_name;

-- MySQL specific
ALTER TABLE employees
DROP PRIMARY KEY;

ALTER TABLE employees
DROP FOREIGN KEY fk_customer_id;

ALTER TABLE employees
DROP INDEX uq_email;

ALTER TABLE employees
DROP CHECK chk_salary;
```

---

### **9. Rename a Constraint**

```sql
-- SQL Server only
EXEC sp_rename 'old_constraint_name', 'new_constraint_name', 'OBJECT';
```

---

### **10. Change Column Default Value**

```sql
-- Set default
ALTER TABLE employees
ALTER COLUMN status SET DEFAULT 'active';

-- Drop default
ALTER TABLE employees
ALTER COLUMN status DROP DEFAULT;
```

---

### **11. Add / Drop Index**

```sql
-- Add index
CREATE INDEX idx_emp_name ON employees(name);

-- Drop index
DROP INDEX idx_emp_name; -- MySQL
DROP INDEX idx_emp_name ON employees; -- SQL Server
```

---

### **12. Reorder Columns (MySQL only)**

```sql
ALTER TABLE employees
MODIFY COLUMN age INT AFTER name;
```
---

### 3. `DROP`
Used to **delete** entire database objects permanently.

**Example:**
```sql
DROP TABLE employees;
```

> ❗ This removes the table *and all its data* permanently.

---

### 4. `TRUNCATE`
Used to **remove all rows** from a table but **retains the table structure** for future use.

**Example:**
```sql
TRUNCATE TABLE employees;
```

> ⚠️ Cannot be rolled back. More efficient than `DELETE` for clearing all data.

---

## 🔍 Differences Between Similar Commands

| Feature         | DELETE                   | TRUNCATE                     | DROP                         |
|----------------|---------------------------|-------------------------------|------------------------------|
| Type           | DML (Data Manipulation)   | DDL                          | DDL                          |
| Removes        | Specific rows             | All rows                     | Entire table (structure + data) |
| Rollback       | ✅ Yes                    | ❌ No                         | ❌ No                        |
| Structure      | Retained                  | Retained                     | Deleted                      |
| Triggers       | Activated                 | Not activated                | Not activated                |
| Speed          | Slower (row by row)       | Faster                       | Fastest                      |

---
