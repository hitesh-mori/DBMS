
---

## **What is `LEAD()` in SQL?**

`LEAD()` is a **window function** that lets you look **forward** in the result set to access a value from a subsequent row — without doing a self-join.

Think of it like *peeking into the future row*.

---

### **Basic Syntax**

```sql
LEAD(column_name, offset, default_value) OVER (PARTITION BY ... ORDER BY ...)
```

* **column\_name** → the column you want to peek at.
* **offset** → how many rows ahead to look (default = 1).
* **default\_value** → what to return if there’s no future row (default = `NULL`).
* **OVER(...)** → defines how rows are ordered and optionally partitioned.

---

### **Simple Example**

**Table: Sales**

| id | month | sales |
| -- | ----- | ----- |
| 1  | Jan   | 1000  |
| 2  | Feb   | 1200  |
| 3  | Mar   | 900   |
| 4  | Apr   | 1100  |

---

**Query:**

```sql
SELECT
    month,
    sales,
    LEAD(sales) OVER (ORDER BY month) AS next_month_sales
FROM Sales;
```

---

**Output:**

| month | sales | next\_month\_sales |
| ----- | ----- | ------------------ |
| Jan   | 1000  | 1200               |
| Feb   | 1200  | 900                |
| Mar   | 900   | 1100               |
| Apr   | 1100  | NULL               |

---

**Explanation:**

* For **Jan**, `LEAD(sales)` looks **1 row ahead** → Feb's sales = `1200`.
* For **Apr**, there is no next row → returns `NULL`.

---

💡 **Real-life use case:**
You could use `LEAD()` to calculate the difference between the current month’s sales and the next month’s sales:

```sql
SELECT
    month,
    sales,
    LEAD(sales) OVER (ORDER BY month) AS next_month_sales,
    LEAD(sales) OVER (ORDER BY month) - sales AS change_next_month
FROM Sales;
```


```sql
select distinct t.ConsecutiveNums
from (

    select 

    case
        when lead(num,0) over (order by id) =  lead(num,1) over (order by id) and
        lead(num,1) over (order by id) = lead(num,2) over (order by id)
        then num
    end as ConsecutiveNums    

from logs    


) as t

where t.ConsecutiveNums is not null

```
