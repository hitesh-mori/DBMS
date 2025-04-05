# 📘 ACID vs CAP in Databases

---

## 🔷 ACID – SQL (Relational) Database Principles

| Property       | Meaning                                                                 |
|----------------|-------------------------------------------------------------------------|
| **A – Atomicity**   | All steps in a transaction are done or none are done.                 |
| **C – Consistency** | The database remains valid before and after the transaction.          |
| **I – Isolation**   | Concurrent transactions don’t interfere with each other.              |
| **D – Durability**  | Committed changes remain even after a crash.                          |

---

## 🔶 CAP Theorem – NoSQL (Distributed) System Constraints

| Property              | Meaning                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| **C – Consistency**       | All nodes show the same data at the same time.                          |
| **A – Availability**      | Every request receives a response, even if not the latest.               |
| **P – Partition Tolerance** | The system continues working even with communication failure.          |

> ⚠️ **CAP Theorem:** You can only choose 2 out of 3 (C, A, P) at any given time.

---

## ⚔️ Comparison Table

| Feature            | ACID (SQL)             | CAP (NoSQL)             |
|--------------------|------------------------|-------------------------|
| Focus              | Data Integrity          | System Trade-offs       |
| Use Case           | Single-node databases   | Distributed databases   |
| Consistency Model  | Strong consistency      | Eventual or tunable     |

---

## 📦 Real-World Examples

- **ACID:** Bank transaction (must be 100% correct).
- **CAP:** WhatsApp messages during network issues (may arrive late, but system is still available).

