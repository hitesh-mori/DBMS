SQL provides several **set operations** that allow combining the results of two or more queries. These include:

- `UNION`
- `UNION ALL`
- `INTERSECT`
- `MINUS` (or `EXCEPT`, depending on the RDBMS)

These operations follow mathematical set theory and are incredibly useful in data comparison and merging.

---

## 🔄 1. UNION

**Combines the result of two SELECT queries and removes duplicates.**

### ✅ Syntax:
```sql
SELECT column1 FROM table1
UNION
SELECT column1 FROM table2;
```

### 📌 Rules:
- Both SELECT queries **must have the same number of columns**.
- Columns must be of **compatible data types**.
- Column names in the result set are taken from the first SELECT query.
- **Duplicates are removed**.

### 💡 Example:
```sql
SELECT name FROM students
UNION
SELECT name FROM teachers;
```

---

## 🔁 2. UNION ALL

**Combines the result of two SELECT queries and retains duplicates.**

### ✅ Syntax:
```sql
SELECT column1 FROM table1
UNION ALL
SELECT column1 FROM table2;
```

### 📌 Rules:
Same as `UNION`, but **does not remove duplicates**.

### 💡 Example:
```sql
SELECT name FROM students
UNION ALL
SELECT name FROM teachers;
```

---

## 🔍 3. INTERSECT *(Not supported in MySQL)*

**Returns only the rows that exist in both SELECT query results.**

### ✅ Syntax:
```sql
SELECT column1 FROM table1
INTERSECT
SELECT column1 FROM table2;
```

### 📌 Rules:
- Same column and type rules as `UNION`.
- **Returns only common rows**.

### 💡 Example:
```sql
SELECT name FROM students
INTERSECT
SELECT name FROM alumni;
```

### ⚠️ MySQL Note:
MySQL does **not** support `INTERSECT` directly. You can emulate it:
```sql
SELECT name FROM students
WHERE name IN (SELECT name FROM alumni);
```

---

## 🚫 4. MINUS / EXCEPT

- `MINUS` is used in **Oracle**.
- `EXCEPT` is used in **PostgreSQL, SQL Server**.

**Returns rows from the first SELECT query that are not in the second SELECT query.**

### ✅ Syntax:
```sql
SELECT column1 FROM table1
MINUS -- or EXCEPT
SELECT column1 FROM table2;
```

### 💡 Example:
```sql
SELECT name FROM students
EXCEPT
SELECT name FROM alumni;
```

### ⚠️ MySQL Alternative:
```sql
SELECT name FROM students
WHERE name NOT IN (SELECT name FROM alumni);
```

---

## ⚖️ Comparison Table

| Operator    | Removes Duplicates | Shows All Matches | MySQL Support |
|-------------|---------------------|--------------------|----------------|
| UNION       | ✅ Yes              | ❌ No              | ✅ Yes         |
| UNION ALL   | ❌ No               | ✅ Yes             | ✅ Yes         |
| INTERSECT   | ✅ Yes              | ❌ No              | ❌ No (Use IN) |
| MINUS       | ✅ Yes              | ❌ No              | ❌ No (Use NOT IN) |

---

## 🎯 Interview Questions with Answers

### 1. **What is the difference between UNION and UNION ALL?**
**A:** UNION removes duplicates; UNION ALL retains all records.

### 2. **Can you use UNION with different column names?**
**A:** Yes, but the number of columns and their data types must match.

### 3. **Which set operation is not supported by MySQL? How do you emulate it?**
**A:** INTERSECT and MINUS are not supported. You can use `IN` and `NOT IN` respectively.

### 4. **When would you use EXCEPT over NOT IN?**
**A:** `EXCEPT` is cleaner and more readable, but `NOT IN` is the alternative in unsupported systems like MySQL.

### 5. **Do set operations affect performance?**
**A:** Yes. `UNION` is slower than `UNION ALL` due to duplicate elimination.

---

## ✅ Best Practices

- Always use `UNION ALL` when duplicates don’t matter—**faster performance**.
- Use `INTERSECT` or `IN` when filtering common rows.
- Use `EXCEPT` or `NOT IN` to detect differences.
- Ensure **column alignment** in number and data types for accurate results.
