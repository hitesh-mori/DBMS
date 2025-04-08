# SQL Date and Time Functions with Examples

Below is a collection of commonly used SQL date and time functions with easy query examples. These examples are based on MySQL syntax.

---

## 1. CURRENT_DATE
Returns the current date.
```sql
SELECT CURRENT_DATE();
-- Output: '2025-04-08'
```

## 2. CURRENT_TIME
Returns the current time.
```sql
SELECT CURRENT_TIME();
-- Output: '14:30:55'
```

## 3. CURRENT_TIMESTAMP / NOW()
Returns the current date and time.
```sql
SELECT CURRENT_TIMESTAMP();
-- Output: '2025-04-08 14:30:55'

SELECT NOW();
-- Output: '2025-04-08 14:30:55'
```

## 4. EXTRACT
Extracts part of a date (like year, month, day).
```sql
SELECT EXTRACT(YEAR FROM '2025-04-08');
-- Output: 2025
```

## 5. DATEDIFF
Returns the number of days between two dates.
```sql
SELECT DATEDIFF('2025-04-10', '2025-04-08');
-- Output: 2
```

## 6. TIMEDIFF
Returns the difference between two time/datetime values.
```sql
SELECT TIMEDIFF('14:30:00', '13:15:00');
-- Output: '01:15:00'
```

## 7. DATE_ADD
Adds a time interval to a date.
```sql
SELECT DATE_ADD('2025-04-08', INTERVAL 5 DAY);
-- Output: '2025-04-13'
```

## 8. DATE_SUB
Subtracts a time interval from a date.
```sql
SELECT DATE_SUB('2025-04-08', INTERVAL 7 DAY);
-- Output: '2025-04-01'
```

## 9. DATE_FORMAT
Formats a date according to the specified format.
```sql
SELECT DATE_FORMAT('2025-04-08', '%W, %M %d, %Y');
-- Output: 'Tuesday, April 08, 2025'
```

---

# Top Interview Questions with Answers

### 1. **What is the difference between CURRENT_DATE and CURRENT_TIMESTAMP?**
**Answer:** `CURRENT_DATE` returns only the date, while `CURRENT_TIMESTAMP` returns both the current date and time.

### 2. **How do you calculate the number of days between two dates?**
**Answer:** Use the `DATEDIFF()` function:
```sql
SELECT DATEDIFF('2025-04-10', '2025-04-08');
```

### 3. **What function do you use to extract the year from a date?**
**Answer:** Use the `EXTRACT()` function:
```sql
SELECT EXTRACT(YEAR FROM '2025-04-08');
```

### 4. **How do you add 1 month to a date in SQL?**
**Answer:** Use `DATE_ADD()`:
```sql
SELECT DATE_ADD('2025-04-08', INTERVAL 1 MONTH);
```

### 5. **What is the use of DATE_FORMAT in SQL?**
**Answer:** `DATE_FORMAT` is used to format the output of a date in a specified style.

### 6. **How to get the current time in SQL?**
**Answer:** Use `CURRENT_TIME()`:
```sql
SELECT CURRENT_TIME();
```

### 7. **What is the difference between NOW() and CURRENT_TIMESTAMP()?**
**Answer:** There is no difference in MySQL; both return the current date and time.

### 8. **How do you subtract days from a date?**
**Answer:** Use `DATE_SUB()`:
```sql
SELECT DATE_SUB('2025-04-08', INTERVAL 7 DAY);
```

### 9. **What does TIMEDIFF() return?**
**Answer:** `TIMEDIFF()` returns the time difference between two datetime or time values.

### 10. **How can you find the month from a date?**
**Answer:** Use:
```sql
SELECT EXTRACT(MONTH FROM '2025-04-08');
```

