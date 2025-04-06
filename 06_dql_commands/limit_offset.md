

## 📘 `LIMIT` and `OFFSET` in SQL

---

### ✅ What is `LIMIT`?

The `LIMIT` clause is used to **restrict the number of rows returned** by a SQL query.

---

### ✅ What is `OFFSET`?

The `OFFSET` clause is used to **skip a specific number of rows** before beginning to return rows from the query.

---

### 📚 Syntax

```sql
SELECT column1, column2
FROM table_name
LIMIT number_of_rows OFFSET offset_value;
```

Or (shorter version):

```sql
SELECT column1, column2
FROM table_name
LIMIT offset_value, number_of_rows;
```

> 📝 Both forms work the same, just a different way to write it.

---

### 📌 Examples

#### 1. Get first 5 rows:

```sql
SELECT * FROM students
LIMIT 5;
```

#### 2. Get next 5 rows after skipping the first 5:

```sql
SELECT * FROM students
LIMIT 5 OFFSET 5;
```

#### 3. Same as above (short form):

```sql
SELECT * FROM students
LIMIT 5, 5;
```

---

### 🧠 Use Case: Pagination

For web apps, `LIMIT` and `OFFSET` are widely used in **pagination**:

```sql
-- Page 1: Records 1 to 10
SELECT * FROM products
LIMIT 10 OFFSET 0;

-- Page 2: Records 11 to 20
SELECT * FROM products
LIMIT 10 OFFSET 10;

-- Page 3: Records 21 to 30
SELECT * FROM products
LIMIT 10 OFFSET 20;
```

---

### ⚠️ Performance Note

- Large `OFFSET` values can **degrade performance** as the engine must scan and skip rows.
- For better performance in large datasets, consider using **indexed cursors or WHERE with indexed `id`**.

---

### 💬 Common Interview Questions

#### 🔹 Q1: What's the difference between `LIMIT 5 OFFSET 10` and `LIMIT 10, 5`?
**A:** They are functionally the same. Both skip the first 10 rows and return the next 5.

#### 🔹 Q2: How would you get the last 5 records of a table?
**A:**
```sql
SELECT * FROM table_name
ORDER BY id DESC
LIMIT 5;
```
Then reverse the result in application if needed.

#### 🔹 Q3: Is OFFSET zero-based or one-based?
**A:** OFFSET is **zero-based**. `OFFSET 0` means start from the very first row.

#### 🔹 Q4: How can you fetch records 21–30?
```sql
SELECT * FROM table_name
LIMIT 10 OFFSET 20;
```

#### 🔹 Q5: Can `OFFSET` be used without `LIMIT`?
**A:** No. MySQL syntax requires `LIMIT` to be used with `OFFSET`.

---

### 🧪 Practice Challenge

Write a query to get the **3rd page** of **10 students each**, sorted alphabetically by name.

```sql
SELECT * FROM students
ORDER BY name
LIMIT 10 OFFSET 20;
```
