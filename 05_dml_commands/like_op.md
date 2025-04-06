

# SQL Pattern Matching: `LIKE`, `NOT LIKE`, Wildcards & Escape Characters

---

## 📘 Introduction

Pattern matching in SQL is performed using the `LIKE` and `NOT LIKE` operators along with wildcard characters. It is primarily used with `WHERE` clauses to filter text data based on partial matching.

---

## 🔹 1. `LIKE` Operator

### ✅ Definition:
The `LIKE` operator is used in a `WHERE` clause to **search for a specified pattern** in a column.

### 🔍 Syntax:
```sql
SELECT * FROM table_name
WHERE column_name LIKE 'pattern';
```

---

## 🔹 2. `NOT LIKE` Operator

### ✅ Definition:
`NOT LIKE` is used to exclude rows that match a certain pattern.

### 🔍 Syntax:
```sql
SELECT * FROM table_name
WHERE column_name NOT LIKE 'pattern';
```

---

## 🔹 3. Wildcard Characters

| Wildcard | Meaning                                 | Example           |
|----------|------------------------------------------|-------------------|
| `%`      | Matches **0 or more characters**         | `'a%'` → "apple"  |
| `_`      | Matches **exactly one character**        | `'a_'` → "an"     |

---

## 🔹 4. Escape Characters

When you want to **search for the literal `%` or `_`**, you must **escape** it using an escape character.

### 🔍 Syntax:
```sql
SELECT * FROM table_name
WHERE column_name LIKE '%\%%' ESCAPE '\';
```

### 📌 Example:
```sql
-- Find any string that contains a literal percent sign (%)
SELECT * FROM products
WHERE description LIKE '%\%%' ESCAPE '\';
```

---

## 🔹 5. Pattern Matching Examples

| Pattern     | Meaning                                 | Matches                       |
|-------------|------------------------------------------|-------------------------------|
| `%a`        | Ends with "a"                            | "India", "Pizza"              |
| `a%`        | Starts with "a"                          | "apple", "anchor"             |
| `%a%`       | Contains "a" anywhere                    | "banana", "cat", "glass"      |
| `_a%`       | Second character is "a"                  | "bat", "car", "man"           |
| `%a_`       | Ends with "a" followed by any one char   | "cap", "map", but not "ca"    |
| `a%b`       | Starts with "a", ends with "b"           | "alphabet", "arb"             |

---

## 🔹 6. Case Sensitivity

- In **MySQL**, `LIKE` is **case-insensitive** by default.
- In **PostgreSQL**, use `ILIKE` for case-insensitive search.
- To force case-sensitivity in MySQL, use `BINARY`:
```sql
SELECT * FROM users WHERE BINARY name LIKE 'A%';
```

---

## 🧠 Hard Theoretical Interview Questions with Answers

---

### 1. **What is the difference between `%` and `_` in SQL pattern matching?**

**Answer:**
- `%` matches **zero or more** characters.
- `_` matches **exactly one** character.

---

### 2. **How would you find names that start with "Jo", contain at least 5 characters, and end with "n"?**

**Answer:**
```sql
SELECT * FROM users
WHERE name LIKE 'Jo__%n';
```
Explanation:
- Starts with `Jo`
- At least 2 more characters (`__`)
- Ends with `n`

---

### 3. **How would you search for strings containing a literal underscore `_` or percent sign `%`?**

**Answer:**
You must use the `ESCAPE` clause.
```sql
SELECT * FROM files WHERE filename LIKE '%\_%' ESCAPE '\';
```
Here, `\_` escapes the underscore.

---

### 4. **What are the performance implications of using `LIKE '%value%'` vs `LIKE 'value%'`?**

**Answer:**
- `LIKE 'value%'` can use **indexes**, hence it's faster.
- `LIKE '%value%'` causes **full table scan**, because the `%` at the start prevents index usage.

---

### 5. **What happens when the pattern in `LIKE` includes only wildcards like `'%'` or `'%%'`?**

**Answer:**
It matches **everything**:
```sql
WHERE name LIKE '%' -- true for all rows
```

---

### 6. **How is `LIKE` different from `=` in SQL?**

**Answer:**
- `=` requires an **exact match**
- `LIKE` allows **pattern-based matching**

Example:
```sql
-- Only matches 'apple'
WHERE fruit = 'apple'

-- Matches 'apple', 'applepie', 'applesauce'
WHERE fruit LIKE 'apple%'
```

---

### 7. **What’s the use of `ILIKE` in PostgreSQL?**

**Answer:**
`ILIKE` is the **case-insensitive version** of `LIKE` in PostgreSQL.

```sql
SELECT * FROM users WHERE name ILIKE 'a%';
```

---

### 8. **Write a query to find all usernames where the second letter is 'a'.**

**Answer:**
```sql
SELECT * FROM users
WHERE username LIKE '_a%';
```

---

### 9. **Can you use wildcards with numeric columns?**

**Answer:**
Yes, but they will be **implicitly converted to strings**. It's not recommended. Use `CAST()` if needed.

---

### 10. **What are the alternatives to `LIKE` for more complex pattern matching?**

**Answer:**
Use `REGEXP` or `RLIKE` (MySQL) or `SIMILAR TO` (PostgreSQL) for **regular expression** support.

---

## ✅ Summary Table

| Operator   | Description                     |
|------------|---------------------------------|
| `LIKE`     | Pattern match using wildcards   |
| `NOT LIKE` | Excludes pattern matches        |
| `%`        | Any number of characters        |
| `_`        | Exactly one character           |
| `ESCAPE`   | Escapes `%` or `_` symbols      |

---

## 🛠️ Best Practices

- Use `LIKE 'abc%'` for better index usage.
- Avoid `%` at the beginning unless necessary.
- Always use `ESCAPE` when dealing with literal `%` or `_`.
- Use `ILIKE` or `BINARY` for case sensitivity when needed.

---

## 📌 Bonus Tip

For more complex searches (like optional characters or repetitions), use:
- `REGEXP` (MySQL)
- `SIMILAR TO` (PostgreSQL)
- Full-text search for advanced indexing and relevance ranking.

---

Let me know if you want this saved as a `.md`, `.pdf`, or `.docx` file.
```
