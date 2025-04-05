
# 📥 Inserting Data in MySQL

The `INSERT INTO` statement is used to insert **new records** into a MySQL table.

---

## 🔹 Insert a Single Row (All Columns)

```sql
INSERT INTO table_name
VALUES (value1, value2, ...);
```

### ✅ Example:
```sql
INSERT INTO users
VALUES (1, "Aryan Mori");
```

> Ensure the **order of values** matches the table schema.

---

## 🔹 Insert a Single Row (Specific Columns)

```sql
INSERT INTO table_name (column1, column2)
VALUES (value1, value2);
```

### ✅ Example:
```sql
INSERT INTO users (id, name)
VALUES (2, "Ankit Mori");
```

> This is safer — you specify the exact columns you're inserting into.

---

## 🔹 Insert Multiple Rows (All Columns)

```sql
INSERT INTO table_name
VALUES (val1_1, val1_2),
       (val2_1, val2_2),
       ...;
```

### ✅ Example:
```sql
INSERT INTO users
VALUES (3, "Raj Patel"),
       (4, "Dev Mehta");
```

---

## 🔹 Insert Multiple Rows (Specific Columns)

```sql
INSERT INTO table_name (column1, column2)
VALUES (val1_1, val1_2),
       (val2_1, val2_2),
       ...;
```

### ✅ Example:
```sql
INSERT INTO users (id, name)
VALUES (5, "Karan Shah"),
       (6, "Neha Joshi");
```

---

## ✅ Insert from Another Table (SELECT INTO)

You can insert values from one table into another:

```sql
INSERT INTO new_table (column1, column2)
SELECT column1, column2 FROM old_table
WHERE condition;
```

### Example:
```sql
INSERT INTO users_backup (id, name)
SELECT id, name FROM users WHERE id < 5;
```

---

## 🛑 Notes:

- If the table has **auto-increment** columns, you can skip those in `INSERT`.
- Avoid inserting duplicate `PRIMARY KEY` or `UNIQUE` values to prevent errors.
- Always match data types with the column definitions.
