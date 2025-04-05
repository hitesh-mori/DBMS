

### 🟢 `SELECT`

Used to **fetch data** from a database table.

```sql
SELECT column1, column2 FROM table_name;
```

**Example:**
```sql
SELECT name, age FROM students;
```

---

### 🟣 `DISTINCT`

Used to **remove duplicates** from the result.

```sql
SELECT DISTINCT column_name FROM table_name;
```

**Example:**
```sql
SELECT DISTINCT department FROM employees;
```

If `department` has repeated values, only unique ones will be shown.

---

### 🔵 `FROM`

Specifies **which table** to pull data from.

```sql
SELECT * FROM table_name;
```

**Example:**
```sql
SELECT * FROM products;
```

---

### 🟡 SQL Aliases (`AS`)

Aliases are used to **rename** columns or tables temporarily **for better readability**.

#### 🔸 Column Alias:
```sql
SELECT column_name AS alias_name FROM table_name;
```

**Example:**
```sql
SELECT name AS student_name FROM students;
```
`student_name` is the alias for the `name` column.

You can **skip `AS`** (it's optional):
```sql
SELECT name student_name FROM students;
```

#### 🔹 Table Alias:
```sql
SELECT t.column_name FROM table_name AS t;
```

**Example:**
```sql
SELECT s.name FROM students AS s;
```
`students` is aliased as `s`.

---

### 🧠 Summary Table

| Keyword   | Purpose                                |
|-----------|----------------------------------------|
| `SELECT`  | Retrieve data                          |
| `DISTINCT`| Remove duplicate rows                  |
| `FROM`    | Specify table                          |
| `AS`      | Create alias for columns or tables     |
