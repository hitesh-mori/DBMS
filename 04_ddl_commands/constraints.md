
## 🔐 SQL **Constraints** — Overview 

SQL **constraints** are rules enforced on columns to maintain **data integrity**. Here are the **main constraints**:

| Constraint   | Description                                                                 |
|--------------|-----------------------------------------------------------------------------|
| `PRIMARY KEY` | Uniquely identifies each row. Cannot be NULL. Can be single or composite. |
| `FOREIGN KEY` | Links a column to the primary key in another table.                       |
| `NOT NULL`    | Ensures the column can't have `NULL` values.                              |
| `UNIQUE`      | Ensures all values in a column are unique.                                |
| `CHECK`       | Limits values based on a condition.                                       |
| `DEFAULT`     | Provides a default value when none is specified.                          |
| `AUTO_INCREMENT` | Automatically increases numeric value. *(MySQL specific)*              |

---

## 🧱 **Primary Key (PK)**

- **Purpose**: Uniquely identifies each row.
- Can be defined:
  - At **column level**:
    ```sql
    id INT PRIMARY KEY
    ```
  - Or **table level**:
    ```sql
    PRIMARY KEY (id)
    ```
  - Can be **composite**:
    ```sql
    PRIMARY KEY (emp_id, dep_id)
    ```
    This means the **combination** must be unique (not individual columns).

✅ **Only one primary key** per table, but it can span **multiple columns**.

---

## 🔗 **Foreign Key (FK)**

- **Purpose**: Enforces a link between **two tables**.
- **Child table** has a column that refers to the **Parent table's primary key**.

```sql
FOREIGN KEY (dep_id) REFERENCES departments(id)
```

---

## 🔄 **Referring vs Referenced Table**

| Term             | Meaning                                      |
|------------------|----------------------------------------------|
| Referenced table | The table being pointed to (i.e. **Parent**) |
| Referring table  | The table that holds the foreign key (**Child**) |

Example:
```sql
-- Referenced table
CREATE TABLE Department (
    id INT PRIMARY KEY,
    name VARCHAR(50)
);

-- Referring table
CREATE TABLE Employee (
    emp_id INT PRIMARY KEY,
    name VARCHAR(50),
    dep_id INT,
    FOREIGN KEY (dep_id) REFERENCES Department(id)
);
```

---

## 🎯 Is Same Data Type Required for FK?

✅ **YES!**
- The foreign key column **must** match the **data type and size** of the primary key it's referencing.
- Example:
  - If `Department.id` is `INT`, then `Employee.dep_id` **must also be INT**.
  - `CHAR(10)` and `VARCHAR(10)` are **not** considered same — they must **exactly match**.

---

## 🔎 Other Constraints

### 1. `NOT NULL`
```sql
name VARCHAR(50) NOT NULL
```
Prevents null values.

---

### 2. `UNIQUE`
```sql
email VARCHAR(100) UNIQUE
```
Ensures no duplicates.

---

### 3. `CHECK`
```sql
age INT CHECK (age >= 18)
```
Condition must be true.

---

### 4. `DEFAULT`
```sql
status VARCHAR(10) DEFAULT 'active'
```
Value assigned if none is provided.

---

### 5. `AUTO_INCREMENT` (MySQL)
```sql
id INT PRIMARY KEY AUTO_INCREMENT
```
Auto-increments numeric values.

---

## 🛠 Ways to Define Constraints

| Method           | Example |
|------------------|---------|
| **Column-level** | `age INT NOT NULL` |
| **Table-level**  | `PRIMARY KEY(id, name)` |

---

## ✅ Summary Table

| Constraint      | Can Be Composite | Null Allowed | Duplicates Allowed | Defined On |
|----------------|------------------|--------------|---------------------|------------|
| `PRIMARY KEY`  | ✅ Yes            | ❌ No         | ❌ No                | Table/Column |
| `FOREIGN KEY`  | ❌ No (usually)   | ✅ Yes        | ✅ Yes               | Table       |
| `UNIQUE`       | ✅ Yes            | ✅ Yes        | ❌ No                | Column      |
| `NOT NULL`     | ❌ No             | ❌ No         | ✅ Yes               | Column      |
| `CHECK`        | ✅ Yes            | ✅ Yes        | ✅ Yes               | Column      |
| `DEFAULT`      | ❌ No             | ✅ Yes        | ✅ Yes               | Column      |

---
