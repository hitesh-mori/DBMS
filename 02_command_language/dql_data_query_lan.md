

---

### 📄 DQL_Commands.md

# 🔎 DQL (Data Query Language)

- DQL is a subset of SQL used to **query** the database and **fetch data**.
- It primarily deals with **reading data** from one or more tables using **SELECT** statements.
- DQL does **not modify** any data or schema — it only retrieves it based on the user's request.

---

## 🔹 DQL Command

### 1. `SELECT`
- The **only** command in DQL.
- Used to **retrieve data** from a database table based on specified conditions.

**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```

**Examples:**

✅ Select all columns:
```sql
SELECT * FROM employees;
```

✅ Select specific columns:
```sql
SELECT name, department FROM employees;
```

✅ With condition:
```sql
SELECT * FROM employees WHERE department = 'HR';
```

✅ With sorting:
```sql
SELECT * FROM employees ORDER BY salary DESC;
```

✅ With aggregation:
```sql
SELECT department, COUNT(*) FROM employees GROUP BY department;
```

---

## 📝 Notes

- DQL is **read-only** — it **does not alter** data.
- Often used in **reporting**, **dashboarding**, or **data analytics**.
- Works with clauses like `WHERE`, `ORDER BY`, `GROUP BY`, `HAVING`, `JOIN`, etc., to fine-tune results.

---