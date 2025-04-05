

# 🔁 TCL (Transaction Control Language)

- TCL commands are used to **manage transactions** in a database.
- Transactions are a sequence of SQL operations performed as a **single logical unit of work**.
- These commands help **ensure data integrity**, especially when multiple users or operations interact with the same data.

---

## 🧩 Key Concepts

- A **transaction** begins when a DML operation (like `INSERT`, `UPDATE`, `DELETE`) is executed.
- A transaction **must end** with either a `COMMIT` or `ROLLBACK`.

---

## 🔹 TCL Commands

### 1. `COMMIT`
- Used to **save** all changes made by the current transaction **permanently** in the database.

**Syntax:**
```sql
COMMIT;
```

**Example:**
```sql
UPDATE employees SET salary = salary + 5000 WHERE department = 'Sales';
COMMIT;
```

---

### 2. `ROLLBACK`
- Used to **undo** changes made in the current transaction **before** they are committed.

**Syntax:**
```sql
ROLLBACK;
```

**Example:**
```sql
DELETE FROM employees WHERE department = 'HR';
ROLLBACK;
```

---

### 3. `SAVEPOINT`
- Used to **set a save point** within a transaction. You can `ROLLBACK` to a savepoint instead of the entire transaction.

**Syntax:**
```sql
SAVEPOINT savepoint_name;
```

**Example:**
```sql
UPDATE employees SET salary = salary + 1000 WHERE id = 1;
SAVEPOINT before_bonus;

UPDATE employees SET salary = salary + 2000 WHERE id = 2;
ROLLBACK TO before_bonus;
```

---

### 4. `RELEASE SAVEPOINT`
- Used to **remove a savepoint** created earlier in the transaction.

**Syntax:**
```sql
RELEASE SAVEPOINT savepoint_name;
```

Note: Not supported in all RDBMS (e.g., MySQL doesn't support it).

---

## 🔁 Summary Table

| Command           | Description                                      | Reversible? |
|------------------|--------------------------------------------------|-------------|
| `COMMIT`         | Saves changes made in the transaction            | ❌ No       |
| `ROLLBACK`       | Undoes changes before commit                     | ✅ Yes      |
| `SAVEPOINT`      | Sets a marker to rollback part of a transaction  | ✅ Yes      |
| `ROLLBACK TO`    | Rolls back to a savepoint                        | ✅ Yes      |
| `RELEASE SAVEPOINT` | Deletes a named savepoint                    | ❌ (Soft)   |

---
