

# 🔐 DCL (Data Control Language)

- DCL commands are used to **control access** to data in a database.
- They help in defining **permissions**, **granting roles**, and **revoking rights**.
- These commands ensure **database security** by managing who can access or manipulate what data.
- DCL is crucial in **multi-user environments**.

---

## 🔹 DCL Commands

### 1. `GRANT`
- Used to **give permissions** to a user on database objects (like tables, views, procedures, etc.).
- You can grant privileges such as SELECT, INSERT, UPDATE, DELETE, etc.

**Syntax:**
```sql
GRANT privilege_name ON object_name TO user_name;
```

**Example:**
```sql
GRANT SELECT, INSERT ON employees TO john;
```

---

### 2. `REVOKE`
- Used to **remove previously granted** permissions from a user.

**Syntax:**
```sql
REVOKE privilege_name ON object_name FROM user_name;
```

**Example:**
```sql
REVOKE INSERT ON employees FROM john;
```

---

## 🔁 Comparison Summary

| Feature        | GRANT                          | REVOKE                         |
|----------------|--------------------------------|--------------------------------|
| Purpose        | Assigns privileges             | Removes privileges             |
| Usage          | Allow users to access data     | Restrict users from access     |
| Impact         | Enables DML/DDL access          | Disables previously granted access |

---
