## 5.3 Window Functions

### 📌 Overview

**Window Functions** allow you to perform calculations across a set of rows **related to the current row**, without collapsing the result like `GROUP BY`.

At companies like Google, window functions are:

* **Heavily used in analytics**
* Common in **SQL interviews**
* Critical for **advanced data transformations**

➡️ They enable powerful operations like:

* Ranking
* Running totals
* Moving averages

---

### 🧠 Key Idea

> Window functions compute values **over a “window” of rows** while still returning **individual rows**

---

### 🧱 Basic Syntax

```sql
FUNCTION() OVER (
    PARTITION BY column
    ORDER BY column
)
```

---

### 🔍 Components Explained

| Component    | Purpose                                    |
| ------------ | ------------------------------------------ |
| FUNCTION()   | The operation (e.g., SUM, RANK)            |
| PARTITION BY | Groups data (like GROUP BY but keeps rows) |
| ORDER BY     | Defines order within partition             |

---

## 🧱 Common Window Functions

---

### 1️⃣ ROW_NUMBER()

* Assigns a unique row number

```sql id="6u6e9c"
SELECT user_id,
       ROW_NUMBER() OVER (PARTITION BY country ORDER BY age DESC) AS rank
FROM users;
```

➡️ Unique ranking per group

---

### 2️⃣ RANK()

* Same rank for ties (skips numbers)

```sql id="7ppcqx"
SELECT user_id,
       RANK() OVER (ORDER BY score DESC) AS rank
FROM users;
```

---

### 3️⃣ DENSE_RANK()

* Same rank for ties (no gaps)

```sql id="v7w7on"
SELECT user_id,
       DENSE_RANK() OVER (ORDER BY score DESC) AS rank
FROM users;
```

---

### ⚖️ Ranking Difference

| Function   | Behavior        |
| ---------- | --------------- |
| ROW_NUMBER | Unique ranking  |
| RANK       | Gaps in ranking |
| DENSE_RANK | No gaps         |

---

### 4️⃣ SUM() OVER (Running Total)

```sql id="lf5mow"
SELECT user_id,
       SUM(amount) OVER (ORDER BY transaction_date) AS running_total
FROM transactions;
```

➡️ Running total across rows

---

### 5️⃣ AVG() OVER (Moving Average)

```sql id="r2j0fz"
SELECT user_id,
       AVG(amount) OVER (ORDER BY transaction_date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS moving_avg
FROM transactions;
```

➡️ Average over a sliding window

---

### 6️⃣ LAG() / LEAD()

* Access previous/next rows

```sql id="x6f8vf"
SELECT user_id,
       amount,
       LAG(amount) OVER (ORDER BY transaction_date) AS prev_amount
FROM transactions;
```

➡️ Compare current vs previous row

---

## 🔄 Window Functions vs GROUP BY

| Aspect      | GROUP BY       | Window Functions   |
| ----------- | -------------- | ------------------ |
| Output      | Collapses rows | Keeps rows         |
| Use Case    | Aggregation    | Row-level analysis |
| Flexibility | Limited        | Very flexible      |

---

### ⚙️ Real-World Example

**Problem:** Find top 2 users per country by score

```sql id="w5l4df"
SELECT *
FROM (
    SELECT user_id,
           country,
           score,
           ROW_NUMBER() OVER (PARTITION BY country ORDER BY score DESC) AS rank
    FROM users
) t
WHERE rank <= 2;
```

➡️ Classic interview question

---

### 🧠 Best Practices

#### 1️⃣ Use PARTITION BY Carefully

* Avoid unnecessary partitions
* Impacts performance

---

#### 2️⃣ Always Define ORDER BY

* Ensures deterministic results

---

#### 3️⃣ Combine with Subqueries

* For filtering (since window functions run after WHERE)

---

### ⚠️ Common Mistakes

* Confusing GROUP BY with window functions
* Missing ORDER BY in ranking
* Using window functions in WHERE (not allowed)
* Not understanding execution order

---

### 🌍 Google-Level Thinking

At Google:

* Window functions are used for:

  * Analytics pipelines
  * User behavior analysis
  * Ranking and segmentation
* Efficient use is critical for:

  * Performance
  * Cost optimization

---

### 🎯 Interview Insight

Interviewers test:

* Ranking problems
* Top-N per group
* Running totals
* Time-based comparisons

Strong candidates:

* Use window functions **cleanly and correctly**
* Avoid overcomplicating solutions

---

### 🧠 Pro Tip

> If you need aggregation **without losing rows**, use a window function.

---

### ✅ Key Takeaways

* Window functions operate over **a set of rows without collapsing them**
* Key functions:

  * ROW_NUMBER, RANK, DENSE_RANK
  * SUM, AVG
  * LAG, LEAD
* Essential for:

  * Advanced analytics
  * SQL interviews
* One of the most powerful tools in SQL—**master it deeply**

---
