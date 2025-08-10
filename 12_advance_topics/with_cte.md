Great question!

### What is `WITH cte AS` in SQL?

`WITH cte AS (...)` defines a **Common Table Expression** (CTE).

---

### What is a CTE?

* A CTE is like a **temporary named result set** (a temporary table) you can reference within your main query.
* It helps organize complex queries by breaking them into simpler parts.
* Improves readability and reusability.
* The CTE exists only during the execution of the query — it’s not stored permanently.

---

### How it works:

```sql
WITH cte AS (
  -- Some complex query here
  SELECT ...
)
SELECT ...
FROM cte
WHERE ...;
```

* The `cte` runs first.
* Then the outer `SELECT` uses the result of `cte` like a table.
* You can have multiple CTEs separated by commas.

---

### Why use CTE?

* To avoid repeating the same subquery.
* To improve readability by giving a subquery a meaningful name.
* To make complex queries modular.

---

### Example:

Suppose you want to get cumulative sums:

```sql
WITH cte AS (
  SELECT
    person_name,
    SUM(weight) OVER (ORDER BY turn) AS cum_weight
  FROM queue
)
SELECT person_name, cum_weight
FROM cte
WHERE cum_weight > 1000;
```

```sql

with cte as(

    select 
        person_name,
        turn,
        sum(weight) over (order by turn) as tw

    from queue
)

select person_name
from cte
where tw <= 1000
order by tw desc
limit 1

```


* `cte` calculates the cumulative weight for each person.
* Outer query filters based on `cum_weight`.

---

If you want, I can also show you how to do it without a CTE!
