
## **1. What is a Transaction in SQL?**

A **transaction** is a logical unit of work in a database that consists of one or more SQL statements executed as a single unit.
Either **all statements succeed** (commit) or **none of them take effect** (rollback).

💡 **Real-life analogy**:
Imagine transferring ₹500 from your account to your friend’s account:

* Step 1: Debit ₹500 from your account.
* Step 2: Credit ₹500 to your friend’s account.
  If step 1 succeeds but step 2 fails, you don’t want money disappearing — so you roll back.

---

## **2. ACID Properties**

| **Property**    | **Meaning**                                           | **Example**                                                  |
| --------------- | ----------------------------------------------------- | ------------------------------------------------------------ |
| **Atomicity**   | All steps succeed or none happen.                     | Money transfer must debit and credit together.               |
| **Consistency** | The database moves from one valid state to another.   | Account balances remain accurate before and after.           |
| **Isolation**   | Transactions are executed independently.              | Two transfers happening at the same time shouldn’t mix data. |
| **Durability**  | Once committed, data is permanent even after failure. | After commit, even if power fails, data remains.             |

---

## **3. Transaction Control Language (TCL) Commands**

| **Command**                   | **Purpose**                                    | **Example**                                     |
| ----------------------------- | ---------------------------------------------- | ----------------------------------------------- |
| **BEGIN / START TRANSACTION** | Starts a transaction.                          | `START TRANSACTION;`                            |
| **COMMIT**                    | Saves all changes.                             | `COMMIT;`                                       |
| **ROLLBACK**                  | Undoes all changes in the current transaction. | `ROLLBACK;`                                     |
| **SAVEPOINT**                 | Creates a checkpoint to roll back partially.   | `SAVEPOINT sp1;`                                |
| **RELEASE SAVEPOINT**         | Removes a savepoint.                           | `RELEASE SAVEPOINT sp1;`                        |
| **SET TRANSACTION**           | Sets isolation level.                          | `SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;` |

---

## **4. Example with Table**

Let’s create a **bank** table.

```sql
CREATE TABLE accounts (
    acc_no INT PRIMARY KEY,
    name VARCHAR(50),
    balance DECIMAL(10,2)
);

INSERT INTO accounts VALUES
(1, 'Hitesh', 5000.00),
(2, 'Ramesh', 3000.00);
```

---

### **Scenario: Transfer ₹1000 from Hitesh to Ramesh**

```sql
START TRANSACTION;

UPDATE accounts SET balance = balance - 1000 WHERE acc_no = 1;
UPDATE accounts SET balance = balance + 1000 WHERE acc_no = 2;

COMMIT;
```

✅ If both updates succeed → `COMMIT` makes them permanent.
❌ If any update fails → `ROLLBACK` reverts all changes.

---

## **5. Using SAVEPOINT**

```sql
START TRANSACTION;

UPDATE accounts SET balance = balance - 500 WHERE acc_no = 1;
SAVEPOINT sp1;

UPDATE accounts SET balance = balance + 500 WHERE acc_no = 2;

ROLLBACK TO sp1; -- Undo second update but keep first

COMMIT;
```

---

## **6. Isolation Levels**

| **Level**            | **Effect**                                             | **Problems Avoided**                          |
| -------------------- | ------------------------------------------------------ | --------------------------------------------- |
| **READ UNCOMMITTED** | Can read uncommitted changes (dirty read).             | None                                          |
| **READ COMMITTED**   | Reads only committed data.                             | Dirty read                                    |
| **REPEATABLE READ**  | Ensures same rows are read again within a transaction. | Dirty read, non-repeatable read               |
| **SERIALIZABLE**     | Fully isolates transactions.                           | Dirty read, non-repeatable read, phantom read |

---

## **7. Common Interview Questions & Answers**

**Q1:** What’s the difference between `ROLLBACK` and `ROLLBACK TO SAVEPOINT`?
**A:** `ROLLBACK` undoes the entire transaction, while `ROLLBACK TO SAVEPOINT` undoes only up to the savepoint, keeping prior changes.

**Q2:** What is the default isolation level in MySQL?
**A:** **REPEATABLE READ**.

**Q3:** What is the difference between COMMIT and AUTO-COMMIT?
**A:** `COMMIT` manually saves changes. Auto-commit saves changes after each statement unless disabled.

**Q4:** Can a transaction have only a single SQL statement?
**A:** Yes, but it’s still treated as a transaction.

**Q5:** Explain "dirty read".
**A:** Reading uncommitted data from another transaction.

---

## **8. Summary Table**

| **Command**         | **When Used**               | **Effect**                  |
| ------------------- | --------------------------- | --------------------------- |
| `START TRANSACTION` | Before multiple operations  | Begin transaction           |
| `COMMIT`            | After successful operations | Save permanently            |
| `ROLLBACK`          | On error/failure            | Undo all                    |
| `SAVEPOINT`         | During long transaction     | Mark partial rollback point |
| `SET TRANSACTION`   | Before execution            | Set isolation level         |

