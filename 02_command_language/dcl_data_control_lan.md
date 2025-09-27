
---

# 🔐 DCL (Data Control Language)

**Definition:**
DCL commands are used to **control access and permissions** in a database. They help manage **security** by defining **who can do what** on database objects (tables, views, procedures, etc.).

* Crucial in **multi-user environments**.
* Ensures only authorized users can **read, modify, or manage data**.

---

## 🔹 Common DCL Commands

### **1. `GRANT`**

* **Purpose:** Gives specific **privileges** to a user or role.
* **Privileges can include:** `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `EXECUTE`, `ALL PRIVILEGES`, etc.

**Syntax:**

```sql
GRANT privilege_list
ON object_name
TO user_name
[WITH GRANT OPTION];
```

**Examples:**

```sql
-- Grant specific privileges
GRANT SELECT, INSERT ON employees TO john;

-- Grant all privileges on a database
GRANT ALL PRIVILEGES ON company_db.* TO admin_user;

-- Grant with ability to give privileges to others
GRANT SELECT ON employees TO manager WITH GRANT OPTION;
```

**Notes:**

* `WITH GRANT OPTION` allows the user to **grant the same privileges to others**.
* Privileges can be granted on **table, database, or entire schema** depending on the DBMS.

---

### **2. `REVOKE`**

* **Purpose:** Removes previously granted **privileges** from a user or role.

**Syntax:**

```sql
REVOKE privilege_list
ON object_name
FROM user_name;
```

**Examples:**

```sql
-- Revoke specific privilege
REVOKE INSERT ON employees FROM john;

-- Revoke all privileges
REVOKE ALL PRIVILEGES ON company_db.* FROM admin_user;
```

**Notes:**

* Revoking removes the ability of the user to perform actions previously allowed.
* Always check which privileges a user currently has before revoking.

---

### **3. Viewing Privileges**

* You can check user privileges using commands or system tables.

**MySQL Example:**

```sql
SHOW GRANTS FOR 'john'@'localhost';
```

**SQL Server Example:**

```sql
SELECT * FROM sys.database_permissions WHERE grantee_principal_id = USER_ID('john');
```

**PostgreSQL Example:**

```sql
\du
```

---

## 🔹 Types of Privileges

* **DDL Privileges:** CREATE, ALTER, DROP, TRUNCATE
* **DML Privileges:** SELECT, INSERT, UPDATE, DELETE
* **EXECUTE Privileges:** EXECUTE (for stored procedures/functions)
* **Administrative Privileges:** GRANT OPTION, REPLICATION, etc.

---

## 🔹 Roles (Optional / Advanced)

* Instead of granting privileges to each user, you can **create a role**, assign privileges to the role, and then assign the role to users.

**Example (PostgreSQL / SQL Server / Oracle):**

```sql
-- Create a role
CREATE ROLE hr_manager;

-- Grant privileges to role
GRANT SELECT, INSERT, UPDATE ON employees TO hr_manager;

-- Assign role to user
GRANT hr_manager TO john;
```

---

## 🔁 GRANT vs REVOKE Comparison

| Feature       | GRANT                                   | REVOKE                              |
| ------------- | --------------------------------------- | ----------------------------------- |
| Purpose       | Assign privileges                       | Remove privileges                   |
| Usage         | Allow users to access data              | Restrict users from access          |
| Impact        | Enables DML/DDL actions                 | Disables previously granted actions |
| Optional flag | WITH GRANT OPTION (delegate privileges) | N/A                                 |

---

## ✅ Key Points

1. DCL **controls access**, it does **not modify data or table structure**.
2. Essential in **multi-user and production environments** to prevent unauthorized access.
3. Always **review granted privileges** periodically.
4. Privileges can be **granted on table, schema, or database level** depending on the DBMS.

