## 5.5 Analytical SQL Patterns

### 📌 Overview

**Analytical SQL Patterns** are reusable query techniques used to solve common data analysis problems.

At companies like Google, these patterns are:

* Frequently used in **real-world analytics**
* Common in **SQL interviews**
* Essential for **business insights and reporting**

➡️ Mastering these patterns helps you solve problems **quickly and efficiently**

---

## 🧱 Core Analytical Patterns

---

### 1️⃣ Top-N per Group

**Problem:** Find top 3 users per country

```sql
SELECT *
FROM (
    SELECT user_id,
           country,
           score,
           ROW_NUMBER() OVER (PARTITION BY country ORDER BY score DESC) AS rank
    FROM users
) t
WHERE rank <= 3;
```

➡️ Uses **window functions + filtering**

---

### 2️⃣ Running Total (Cumulative Sum)

**Problem:** Calculate cumulative sales over time

```sql
SELECT date,
       SUM(sales) OVER (ORDER BY date) AS running_total
FROM sales;
```

➡️ Useful for trend analysis

---

### 3️⃣ Moving Average

**Problem:** Smooth fluctuations in data

```sql
SELECT date,
       AVG(sales) OVER (
           ORDER BY date
           ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
       ) AS moving_avg
FROM sales;
```

➡️ Helps identify trends

---

### 4️⃣ Deduplication (Remove Duplicates)

**Problem:** Keep latest record per user

```sql
SELECT *
FROM (
    SELECT *,
           ROW_NUMBER() OVER (PARTITION BY user_id ORDER BY updated_at DESC) AS rn
    FROM users
) t
WHERE rn = 1;
```

➡️ Very common in data pipelines

---

### 5️⃣ Ranking & Leaderboards

**Problem:** Rank users by score

```sql
SELECT user_id,
       RANK() OVER (ORDER BY score DESC) AS rank
FROM users;
```

---

### 6️⃣ Percentiles / Distribution

**Problem:** Divide users into quartiles

```sql
SELECT user_id,
       NTILE(4) OVER (ORDER BY score DESC) AS quartile
FROM users;
```

➡️ Used for segmentation

---

### 7️⃣ Sessionization

**Problem:** Group user events into sessions

```sql
SELECT user_id,
       event_time,
       SUM(is_new_session) OVER (PARTITION BY user_id ORDER BY event_time) AS session_id
FROM (
    SELECT *,
           CASE 
               WHEN TIMESTAMP_DIFF(event_time,
                                   LAG(event_time) OVER (PARTITION BY user_id ORDER BY event_time),
                                   MINUTE) > 30
               THEN 1 ELSE 0
           END AS is_new_session
    FROM events
) t;
```

➡️ Common in user behavior analysis

---

### 8️⃣ Funnel Analysis

**Problem:** Track user progression through steps

```sql
SELECT
    COUNT(DISTINCT user_id) AS step1,
    COUNT(DISTINCT CASE WHEN step = 2 THEN user_id END) AS step2
FROM events;
```

➡️ Used in product analytics

---

### 9️⃣ Cohort Analysis

**Problem:** Analyze user retention over time

```sql
SELECT cohort_month,
       activity_month,
       COUNT(DISTINCT user_id) AS active_users
FROM user_activity
GROUP BY cohort_month, activity_month;
```

➡️ Measures retention trends

---

### 🔄 Pattern Summary

| Pattern         | Use Case                  |
| --------------- | ------------------------- |
| Top-N per group | Ranking within categories |
| Running total   | Time-based accumulation   |
| Moving average  | Trend smoothing           |
| Deduplication   | Removing duplicates       |
| Ranking         | Leaderboards              |
| Percentiles     | Segmentation              |
| Sessionization  | User sessions             |
| Funnel          | Conversion tracking       |
| Cohort          | Retention analysis        |

---

### 🧠 Key Concepts Behind Patterns

* Window functions
* Aggregations
* Conditional logic (CASE)
* Time-based operations

➡️ Most patterns are combinations of these

---

### ⚙️ Real-World Example

**Problem:** Find top 2 products per category by sales

```sql
SELECT *
FROM (
    SELECT product_id,
           category,
           SUM(sales) AS total_sales,
           ROW_NUMBER() OVER (PARTITION BY category ORDER BY SUM(sales) DESC) AS rank
    FROM products
    GROUP BY product_id, category
) t
WHERE rank <= 2;
```

---

### 🌍 Google-Level Usage

At Google:

* Analytical patterns are used for:

  * Ads performance analysis
  * User behavior tracking
  * Product metrics
* Queries often run on:

  * Massive datasets (TB–PB)

➡️ Efficiency + correctness are critical

---

### ⚠️ Common Mistakes

* Not using window functions when needed
* Overcomplicating queries
* Ignoring performance impact
* Incorrect partitioning or ordering

---

### 🎯 Interview Insight

Interviewers often ask:

* Top-N problems
* Deduplication
* Running totals
* Sessionization

Strong candidates:

* Recognize patterns quickly
* Apply correct SQL constructs
* Write clean, optimized queries

---

### 🧠 Pro Tip

> Most SQL interview questions are just **variations of a few core patterns**

---

### ✅ Key Takeaways

* Analytical SQL patterns are **reusable problem-solving templates**
* Master:

  * Window functions
  * Aggregations
  * CASE logic
* Common patterns:

  * Ranking, deduplication, running totals
* Critical for:

  * Real-world analytics
  * SQL interviews

---
