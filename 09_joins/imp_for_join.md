
# MySQL Foreign Key Cheat Sheet

## 📌 Creating a Foreign Key with a Custom Name

```sql
CREATE TABLE department (
  id INT PRIMARY KEY,
  name VARCHAR(50),
  hod_id INT,
  CONSTRAINT fk_hod FOREIGN KEY (hod_id) REFERENCES teacher(id)
);
```

## ➕ Adding a Foreign Key After Table Creation

```sql
ALTER TABLE department
ADD CONSTRAINT fk_hod FOREIGN KEY (hod_id)
REFERENCES teacher(id)
ON DELETE SET NULL;
```

## ❌ Deleting a Foreign Key Constraint

First, find the foreign key name:

```sql
SELECT CONSTRAINT_NAME
FROM information_schema.KEY_COLUMN_USAGE
WHERE TABLE_NAME = 'department';
```

Then drop it:

```sql
ALTER TABLE department DROP FOREIGN KEY fk_hod;
```

## 🔄 Modifying a Foreign Key Constraint

MySQL does not allow direct modification. You need to:

1. Drop the existing foreign key.
2. Add a new one with the desired rule:

```sql
ALTER TABLE department DROP FOREIGN KEY fk_hod;

ALTER TABLE department
ADD CONSTRAINT fk_hod FOREIGN KEY (hod_id)
REFERENCES teacher(id)
ON DELETE CASCADE;
```

## ⚙️ ON DELETE Options

| Option       | Behavior                                                                 |
|--------------|--------------------------------------------------------------------------|
| `CASCADE`    | Deletes the child rows automatically when the parent row is deleted.     |
| `SET NULL`   | Sets the foreign key column in child table to NULL on parent deletion.   |
| `RESTRICT`   | Prevents deletion of the parent if there are matching child rows.        |
| `NO ACTION`  | Same as `RESTRICT` in MySQL.                                             |

---

# 👨‍💼 Interview Questions & Answers

### 1. What is a foreign key in MySQL?
A foreign key is a field (or collection of fields) in one table that uniquely identifies a row in another table. It establishes a relationship between the two tables.

---

### 2. What are the different `ON DELETE` actions?

- **CASCADE**: Deletes child records when the parent is deleted.
- **SET NULL**: Sets foreign key to NULL when the parent is deleted.
- **RESTRICT**/**NO ACTION**: Prevents deletion if there are dependent rows.

---

### 3. How can you modify an existing foreign key?

You can't modify directly. Drop the old one and create a new foreign key with the desired options.

---

### 4. How to find the foreign key constraint name?

Use this:

```sql
SELECT CONSTRAINT_NAME
FROM information_schema.KEY_COLUMN_USAGE
WHERE TABLE_NAME = 'your_table_name';
```

---

### 5. What is the default behavior if `ON DELETE` is not specified?

If not specified, MySQL uses `RESTRICT` or `NO ACTION` by default, which blocks deletion of parent rows with dependent child rows.

---

### 6. Can you create a foreign key referencing a non-primary key column?

Yes, but the referenced column must have a `UNIQUE` constraint or be a `PRIMARY KEY`.

---

### 7. What's the difference between `RESTRICT` and `NO ACTION`?

In MySQL, there's no difference between `RESTRICT` and `NO ACTION` — both prevent deletion if child rows exist.

---

### 8. Can a table have multiple foreign keys?

Yes, a table can have multiple foreign keys referencing different tables or even the same table.

---

## 🧪 Pro Tip

If you're testing your schema a lot, use `ON DELETE CASCADE` for easy cleanup. For real applications, choose `RESTRICT` or `SET NULL` carefully depending on data integrity needs.

```
