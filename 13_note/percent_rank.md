
---

## **1️⃣ What is `percent_rank()`?**

`percent_rank()` is a **window function** that calculates the **relative rank of a row within a partition**, scaled between **0 and 1**.

* **0** → lowest value in the partition
* **1** → highest value in the partition (or close to 1 depending on number of rows)
* Values in between → relative position among other rows

**formula:**

[
percent_rank = \frac{rank - 1}{total_rows - 1}
]

where `rank` is the **rank of the row within the partition** (starting from 1), and `total_rows` is the total number of rows in the partition.

---

## **2️⃣ Basic Example**

Suppose we have a table of claims:

| policy_num | state | fraud_score |
| ---------- | ----- | ----------- |
| A1         | CA    | 0.2         |
| A2         | CA    | 0.5         |
| A3         | CA    | 0.7         |
| A4         | CA    | 0.9         |

---

### Query:

```sql
select
    policy_num,
    state,
    fraud_score,
    rank() over(partition by state order by fraud_score) as rnk,
    percent_rank() over(partition by state order by fraud_score) as pr
from claims
where state = 'CA';
```

---

### **Step by step calculation**

1. **Order by fraud_score (ascending):**

| policy_num | fraud_score | rank |
| ---------- | ----------- | ---- |
| A1         | 0.2         | 1    |
| A2         | 0.5         | 2    |
| A3         | 0.7         | 3    |
| A4         | 0.9         | 4    |

2. **Calculate percent_rank**:

[
percent_rank = \frac{rank - 1}{total_rows - 1} = \frac{rank - 1}{4-1} = \frac{rank - 1}{3}
]

| policy_num | fraud_score | rank | percent_rank |
| ---------- | ----------- | ---- | ------------ |
| A1         | 0.2         | 1    | 0/3 = 0      |
| A2         | 0.5         | 2    | 1/3 ≈ 0.333  |
| A3         | 0.7         | 3    | 2/3 ≈ 0.667  |
| A4         | 0.9         | 4    | 3/3 = 1      |

---

### ✅ **Observations**

* The **lowest fraud_score** gets 0.
* The **highest fraud_score** gets 1.
* All others are scaled **linearly** between 0 and 1.
* This makes it **easy to filter top 5%, 10%, etc.**, using a simple `where pr >= 0.95` or `pr <= 0.05`.

---

## **3️⃣ Using percent_rank to get top 5% fraud scores**

```sql
select policy_num, state, claim_cost, fraud_score
from (
    select *,
           percent_rank() over (partition by state order by fraud_score) as pr
    from fraud_score
) t
where pr >= 0.95
order by state, fraud_score desc;
```

* `partition by state` → calculates percent_rank **separately for each state**.
* `order by fraud_score` → higher fraud_score → higher pr.
* `pr >= 0.95` → selects **top 5% of claims in each state**.

---

## **4️⃣ Notes**

* `percent_rank()` differs from `rank()` and `dense_rank()`:

  * `rank()` → gives absolute position (can have gaps for ties)
  * `dense_rank()` → gives absolute position (no gaps)
  * `percent_rank()` → normalized between 0–1 → perfect for **percentile calculations**

* Ties share the same rank, and `percent_rank()` will reflect that.


