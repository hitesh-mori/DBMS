
# SQL COALESCE Function

The **`COALESCE`** function in SQL is used to handle `NULL` values.  
It returns the **first non-NULL value** from the list of arguments provided.


## Syntax

```sql
COALESCE(expr1, expr2, expr3, ..., exprN)
````

* `expr1, expr2, ..., exprN` → list of expressions.
* The function checks each expression **from left to right** and returns the first one that is not `NULL`.
* If all expressions are `NULL`, it returns `NULL`.

---

## Example 1: Basic Usage

```sql
SELECT COALESCE(NULL, NULL, 'Hello', 'World') AS result;
```

**Output:**

```
result
------
Hello
```

---

## Example 2: Handling NULL in a Table

Suppose we have a table `employee`:

| id | name   | bonus |
| -- | ------ | ----- |
| 1  | Akshay | 5000  |
| 2  | Tirth  | NULL  |
| 3  | Jeel   | 3000  |
| 4  | Harvy  | NULL  |

Query:

```sql
SELECT 
    id,
    name,
    COALESCE(bonus, 0) AS final_bonus
FROM employee;
```

**Output:**

| id | name   | final\_bonus |
| -- | ------ | ------------ |
| 1  | Akshay | 5000         |
| 2  | Tirth  | 0            |
| 3  | Jeel   | 3000         |
| 4  | Harvy  | 0            |

Here, `NULL` bonus values are replaced with `0`.

---

## Example 3: Multiple Fallbacks

```sql
SELECT 
    name,
    COALESCE(phone, email, 'Contact Not Available') AS contact_info
FROM employee;
```

This query returns:

* `phone` if available,
* otherwise `email`,
* otherwise `'Contact Not Available'`.

---

## Key Notes

* `COALESCE` is ANSI SQL standard, works across databases (MySQL, PostgreSQL, SQL Server, Oracle, etc.).
* It is often used in **data cleaning** and **report generation**.
* It is functionally similar to `ISNULL` (SQL Server) or `IFNULL` (MySQL), but more flexible since it can take multiple arguments.

---


