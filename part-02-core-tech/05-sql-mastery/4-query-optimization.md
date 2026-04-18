## 5.4 Query Optimization

### 📌 Overview

**Query Optimization** is the process of making SQL queries:

* Faster ⚡
* More efficient 💾
* Cost-effective 💰

At companies like Google, queries often run on **terabytes to petabytes of data**, so inefficient queries can:

* Increase latency
* Waste compute resources
* Cost thousands of dollars

➡️ Optimization is not optional—it’s **critical at scale**

---

### 🧠 Optimization Mindset

> The best query is not just correct—it’s **efficient**

Always think:

* How much data is being scanned?
* Can I reduce work early?
* Is this query scalable?

---

### 🧱 Core Optimization Techniques

---

#### 1️⃣ Select Only Required Columns

```sql
-- ❌ Inefficient
SELECT * FROM users;

-- ✅ Optimized
SELECT user_id, name FROM users;
```

➡️ Reduces data scanned and improves performance

---

#### 2️⃣ Filter Early (Predicate Pushdown)

```sql
SELECT user_id
FROM users
WHERE country = 'US';
```

➡️ Apply filters as early as possible to reduce dataset size

---

#### 3️⃣ Use Proper Indexing (Where Applicable)

* Indexes speed up lookups

```sql
SELECT * FROM users WHERE user_id = 123;
```

➡️ Fast with index, slow without

> Note: In systems like BigQuery, indexing is replaced by **partitioning & clustering**

---

#### 4️⃣ Partitioning & Clustering

* Partition tables by date or key

```sql
SELECT *
FROM events
WHERE event_date = '2025-01-01';
```

➡️ Only scans relevant partitions

---

#### 5️⃣ Avoid Unnecessary Joins

* Join only when needed
* Reduce dataset before joining

```sql
-- Filter before join
SELECT *
FROM users u
JOIN orders o
ON u.user_id = o.user_id
WHERE u.country = 'US';
```

---

#### 6️⃣ Use Aggregation Efficiently

* Avoid grouping large datasets unnecessarily

```sql
SELECT country, COUNT(*)
FROM users
GROUP BY country;
```

➡️ Combine with filtering to reduce workload

---

#### 7️⃣ Avoid Subqueries When Joins Are Better

```sql
-- ❌ Subquery
SELECT name
FROM users
WHERE user_id IN (SELECT user_id FROM orders);

-- ✅ Join
SELECT DISTINCT u.name
FROM users u
JOIN orders o
ON u.user_id = o.user_id;
```

➡️ Joins are often more efficient

---

#### 8️⃣ Limit Data Early

```sql
SELECT *
FROM users
LIMIT 100;
```

➡️ Useful for exploration, not final production queries

---

#### 9️⃣ Use Window Functions Carefully

* Expensive on large datasets
* Combine with filtering and partitioning

---

#### 🔟 Avoid Repeated Computations

* Use CTEs (Common Table Expressions)

```sql
WITH filtered_users AS (
    SELECT * FROM users WHERE country = 'US'
)
SELECT COUNT(*) FROM filtered_users;
```

➡️ Improves readability and avoids recomputation

---

### 🔄 Query Execution Awareness

```text
FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY
```

➡️ Filtering early (WHERE) is key to optimization

---

### ⚙️ Before vs After Optimization

#### ❌ Inefficient

```sql
SELECT *
FROM users
WHERE LOWER(country) = 'us';
```

➡️ Prevents index/partition usage

---

#### ✅ Optimized

```sql
SELECT user_id, name
FROM users
WHERE country = 'US';
```

---

### 🧠 Big Data Optimization Principles

* **Scan less data**
* **Move less data**
* **Compute efficiently**

---

### 🌍 Google-Level Optimization

At Google:

* Engineers optimize for:

  * Query cost (BigQuery pricing)
  * Latency (user-facing systems)
* Techniques:

  * Partition pruning
  * Efficient joins
  * Query rewriting

➡️ Even small improvements can save **millions at scale**

---

### ⚠️ Common Mistakes

* Using `SELECT *`
* Filtering late (after joins)
* Ignoring partitioning
* Overusing subqueries
* Applying functions in WHERE (breaks optimization)

---

### 🎯 Interview Insight

Interviewers expect:

* Ability to:

  * Identify inefficient queries
  * Suggest improvements
* Understanding of:

  * Data scanning
  * Execution order

Strong candidates:

* Explain **why a query is inefficient**
* Propose **better alternatives**

---

### 🧠 Pro Tip

> The fastest query is the one that processes the **least amount of data**

---

### ✅ Key Takeaways

* Query optimization = **performance + cost efficiency**
* Focus on:

  * Filtering early
  * Reducing data scanned
  * Efficient joins
* Understand:

  * Execution order
  * Partitioning strategies
* Critical for:

  * Big Data systems
  * SQL interviews

---
