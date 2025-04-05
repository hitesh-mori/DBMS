
# 📁 DATABASE OPERATIONS

### ✅ 1. Create a New Database

```sql
CREATE DATABASE database_name;
```

> 💡 Creates a new database with the given name.

---

### 🔍 2. Show All Databases

```sql
SHOW DATABASES;
```

> 💡 Lists all available databases.

---

### 🗑️ 3. Drop/Delete a Database

```sql
DROP DATABASE database_name;
```

> 💡 Deletes the entire database and all of its tables permanently.

---

### 🧭 4. Use a Specific Database

```sql
USE database_name;
```

> 💡 Switches context to the specified database to perform operations inside it.

---

# 🗂️ TABLE OPERATIONS

---

## 🧱 5. Create Table

```sql
CREATE TABLE table_name (
    column1 datatype constraints,
    column2 datatype constraints,
    ...
);
```

### 🧠 Example:

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    salary DECIMAL(10, 2)
);
```

---

## 📌 Rules for Table & Column Naming (SQL Name Conventions)

| Rule | Description |
|------|-------------|
| ✅ Must start with a letter | e.g., `table1`, not `1table` |
| ✅ Can include letters, numbers, underscores | Avoid spaces or special characters |
| ❌ No reserved keywords | e.g., don’t name a column `select` or `from` |
| 🔠 Case-insensitive | SQL is usually case-insensitive |
| 📏 Keep it meaningful | Use descriptive names like `employee_salary` not `es` |

---

## 🔍 6. Describe a Table (View Schema)

```sql
DESCRIBE table_name;
-- or
DESC table_name;
```

> 💡 Shows column names, types, keys, nullability, and default values.

---

# 📋 CREATE TABLE FROM ANOTHER TABLE

There are multiple ways to do this:

---

### 🆕 1. Create Table with Structure Only (No Data)

```sql
CREATE TABLE new_table
AS
SELECT * FROM old_table
WHERE 1 = 0;
```

> 💡 Creates a table with the same columns as `old_table` but copies no data.

---

### 🆕 2. Create Table with Structure + Data (All Columns, All Rows)

```sql
CREATE TABLE new_table
AS
SELECT * FROM old_table;
```

> ✅ Copies both structure and all data from `old_table`.

---

### 🆕 3. Create Table with Specific Columns Only

```sql
CREATE TABLE new_table
AS
SELECT column1, column2 FROM old_table;
```

> ✅ Copies only selected columns and their data.

---

### 🆕 4. Create Table with Selected Data Only (Using `WHERE`)

```sql
CREATE TABLE new_table
AS
SELECT * FROM old_table WHERE age > 30;
```

> ✅ Copies full structure, but only filtered data based on condition.

---

### 🆕 5. Copy Table Structure Using `LIKE` (No Data)

```sql
CREATE TABLE new_table LIKE old_table;
```

> ✅ Copies exact structure including indexes and constraints.
