## 5.6 Real Interview SQL Questions

### 📌 Overview

SQL interviews at companies like Google focus on:

* Real-world data problems
* Analytical thinking
* Query correctness + efficiency

➡️ Most questions are **variations of core patterns**:

* Joins
* Aggregations
* Window functions
* Data cleaning

---

## 🧠 How to Approach SQL Interviews

```text
1. Understand the problem
2. Clarify edge cases
3. Write a basic query
4. Optimize if needed
5. Validate with examples
```

---

## 🧱 Common Interview Questions

---

### 1️⃣ Top N Per Group

**Problem:** Find top 3 highest-paid employees per department

```sql
SELECT *
FROM (
    SELECT employee_id,
           department,
           salary,
           ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS rank
    FROM employees
) t
WHERE rank <= 3;
```

💡 Tests: **Window functions + ranking**

---

### 2️⃣ Find Duplicate Records

**Problem:** Find duplicate emails

```sql
SELECT email
FROM users
GROUP BY email
HAVING COUNT(*) > 1;
```

💡 Tests: **GROUP BY + HAVING**

---

### 3️⃣ Running Total

**Problem:** Calculate cumulative revenue

```sql
SELECT date,
       SUM(revenue) OVER (ORDER BY date) AS running_total
FROM sales;
```

💡 Tests: **Window functions**

---

### 4️⃣ User Retention (Cohort Style)

**Problem:** Count users who returned the next day

```sql
SELECT COUNT(DISTINCT a.user_id)
FROM activity a
JOIN activity b
ON a.user_id = b.user_id
AND DATE_ADD(a.date, INTERVAL 1 DAY) = b.date;
```

💡 Tests: **Self-join + date logic**

---

### 5️⃣ Second Highest Salary

```sql
SELECT MAX(salary)
FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);
```

💡 Tests: **Subquery logic**

---

### 6️⃣ Deduplicate Records

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

💡 Tests: **Window function + filtering**

---

### 7️⃣ Find Missing Data

**Problem:** Find customers with no orders

```sql
SELECT u.user_id
FROM users u
LEFT JOIN orders o
ON u.user_id = o.user_id
WHERE o.user_id IS NULL;
```

💡 Tests: **LEFT JOIN + NULL filtering**

---

### 8️⃣ Sessionization (Advanced)

**Problem:** Identify user sessions

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

💡 Tests: **LAG + window functions**

---

### 9️⃣ Funnel Analysis

**Problem:** Count users completing steps

```sql
SELECT
    COUNT(DISTINCT user_id) AS step1,
    COUNT(DISTINCT CASE WHEN step = 2 THEN user_id END) AS step2
FROM events;
```

💡 Tests: **Conditional aggregation**

---

### 🔄 Pattern Mapping

| Question Type  | Pattern            |
| -------------- | ------------------ |
| Top-N          | Window functions   |
| Duplicates     | GROUP BY           |
| Running totals | Window functions   |
| Retention      | Self-join          |
| Deduplication  | ROW_NUMBER         |
| Missing data   | LEFT JOIN          |
| Sessions       | LAG + window       |
| Funnel         | CASE + aggregation |

---

### 🧠 Key Skills Tested

* SQL fundamentals
* Joins and subqueries
* Window functions
* Edge case handling
* Query optimization

---

### ⚙️ Real Interview Expectations

At Google:

* Write **correct queries quickly**
* Explain:

  * Logic
  * Trade-offs
* Handle:

  * Edge cases
  * Large data scenarios

---

### ⚠️ Common Mistakes

* Not clarifying requirements
* Ignoring NULLs
* Using wrong join type
* Overcomplicating queries
* Not optimizing

---

### 🎯 Pro Tips

* Start simple, then optimize
* Speak your thought process
* Use aliases for clarity
* Test logic with small examples

---

### 🧠 Interview Strategy

> Recognize the pattern → Apply the correct SQL technique → Keep it clean and efficient

---

### ✅ Key Takeaways

* Most SQL interview questions follow **repeatable patterns**
* Master:

  * Window functions
  * Joins
  * Aggregations
* Practice:

  * Real-world scenarios
* Strong SQL skills are **one of the biggest hiring signals in Data Engineering interviews**

---
