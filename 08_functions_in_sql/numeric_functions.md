

# 📊 MySQL Numeric Functions – Explained with Examples

---

## 🔢 1. `CEIL(x)` / `CEILING(x)`
Returns the smallest integer greater than or equal to `x`.

```sql
SELECT CEIL(5.3);    -- 6
SELECT CEIL(-2.7);   -- -2
```

---

## 🧮 2. `ROUND(x, d)`
Rounds `x` to `d` decimal places.

```sql
SELECT ROUND(3.14159, 2);   -- 3.14
SELECT ROUND(5.678);        -- 6
```

---

## ➕ 3. `ABS(x)`
Returns the absolute (non-negative) value of `x`.

```sql
SELECT ABS(-10);    -- 10
SELECT ABS(8);      -- 8
```

---

## ⬇️ 4. `FLOOR(x)`
Returns the largest integer less than or equal to `x`.

```sql
SELECT FLOOR(5.9);    -- 5
SELECT FLOOR(-2.1);   -- -3
```

---

## ➗ 5. `MOD(x, y)`
Returns the remainder of `x / y`.

```sql
SELECT MOD(10, 3);    -- 1
SELECT 13 % 5;        -- 3 (alternative syntax)
```

---

## 🔌 6. `POWER(x, y)`
Returns `x` raised to the power `y`.

```sql
SELECT POWER(2, 3);    -- 8
SELECT POWER(5, 0);    -- 1
```

---

## 🧠 7. `SQRT(x)`
Returns the square root of `x`.

```sql
SELECT SQRT(25);     -- 5
SELECT SQRT(2);      -- 1.4142...
```

---

## 🔝 8. `GREATEST(x1, x2, ...)`
Returns the largest of the input values.

```sql
SELECT GREATEST(10, 5, 8, 23);   -- 23
```

---

## 🔽 9. `LEAST(x1, x2, ...)`
Returns the smallest of the input values.

```sql
SELECT LEAST(10, 5, 8, 23);   -- 5
```

---

## 🎲 10. `RAND()`
Returns a random float between 0 and 1.

```sql
SELECT RAND();        -- Example: 0.32822
```

---

# 🧠 Top 10 Hardest Questions (with SQL Answers)

---

### 1. ✅ **Find the product of the two largest numbers among 4 columns in a table.**

```sql
SELECT id,
       GREATEST(col1, col2, col3, col4) * 
       GREATEST(LEAST(col1, col2, col3, col4),
                GREATEST(LEAST(col1, col2), LEAST(col3, col4))
       ) AS product
FROM my_table;
```

---

### 2. ✅ **Round the square root of each number to 2 decimal places and return only those > 3.5**

```sql
SELECT number, ROUND(SQRT(number), 2) AS rounded_sqrt
FROM numbers
WHERE ROUND(SQRT(number), 2) > 3.5;
```

---

### 3. ✅ **Display only rows where the ceiling and floor of a value are the same (i.e., integers)**

```sql
SELECT value
FROM my_table
WHERE CEIL(value) = FLOOR(value);
```
---

### 4. ✅ **Find the absolute difference between max and min salary from an employee table**

```sql
SELECT ABS(MAX(salary) - MIN(salary)) AS salary_diff
FROM employees;
```

---

### 5. ✅ **List all rows where the modulo of two columns results in a prime number**

```sql
SELECT *
FROM my_table
WHERE MOD(col1, col2) IN (2, 3, 5, 7, 11, 13, 17, 19);
```

---

### 6. ✅ **Select customers with total purchases rounded to nearest 1000 and filter by greatest value**

```sql
SELECT customer_id, ROUND(SUM(amount), -3) AS rounded_total
FROM purchases
GROUP BY customer_id
HAVING rounded_total = (
  SELECT MAX(ROUND(SUM(amount), -3))
  FROM purchases
  GROUP BY customer_id
);
```

---

### 7. ✅ **Generate 10 random numbers between 1 and 100 in a SELECT query**

```sql
SELECT FLOOR(1 + (RAND() * 100)) AS random_number
FROM dual
LIMIT 10;
```

> For 10 values, use a dummy numbers table or:
```sql
SELECT FLOOR(1 + (RAND() * 100)) AS rand_num
FROM (SELECT 1 UNION SELECT 2 UNION SELECT 3 UNION SELECT 4 UNION SELECT 5 
      UNION SELECT 6 UNION SELECT 7 UNION SELECT 8 UNION SELECT 9 UNION SELECT 10) AS t;
```

---

### 8. ✅ **Find numbers in a table that are equal to their square root raised to 2 (i.e., perfect squares)**

```sql
SELECT num
FROM numbers
WHERE ROUND(SQRT(num), 0) * ROUND(SQRT(num), 0) = num;
```

---

### 9. ✅ **Find the least price greater than 100 from a list using LEAST and CASE**

```sql
SELECT LEAST(
    CASE WHEN price1 > 100 THEN price1 ELSE 99999 END,
    CASE WHEN price2 > 100 THEN price2 ELSE 99999 END,
    CASE WHEN price3 > 100 THEN price3 ELSE 99999 END
) AS least_price_gt_100
FROM prices;
```

---

### 10. ✅ **Sort records by the rounded power of two columns (e.g., POWER(col1, col2)) in descending order**

```sql
SELECT *,
       ROUND(POWER(col1, col2), 2) AS power_val
FROM my_table
ORDER BY power_val DESC;
```
