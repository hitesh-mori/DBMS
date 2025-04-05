
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

---

### 2. `ALTER`
Used to **modify the structure** of existing database objects.

**Examples:**
- Add a column:
```sql
ALTER TABLE employees ADD age INT;
```
- Rename a column:
```sql
ALTER TABLE employees RENAME COLUMN id TO employee_id;
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
