## 5.2 Joins and Subqueries

### 📌 Overview

**Joins and Subqueries** are essential SQL techniques used to:

* Combine data from multiple tables
* Perform complex filtering and transformations

At companies like Google, these are **heavily tested** because real-world data is:

* Distributed across tables
* Interconnected

➡️ Mastering them is critical for **real-world querying and interviews**

---

## 🧱 JOINS

### 🧠 What is a Join?

A **JOIN** combines rows from two or more tables based on a related column (key).

---

### 🔗 Types of Joins

#### 1️⃣ INNER JOIN (Most Common)

* Returns only matching rows

```sql
SELECT u.name, o.order_id
FROM users u
INNER JOIN orders o
ON u.user_id = o.user_id;
```

➡️ Only users who have orders

---

#### 2️⃣ LEFT JOIN (LEFT OUTER JOIN)

* Returns all rows from left table + matching rows from right

```sql
SELECT u.name, o.order_id
FROM users u
LEFT JOIN orders o
ON u.user_id = o.user_id;
```

➡️ Includes users with no orders (NULLs)

---

#### 3️⃣ RIGHT JOIN

* Opposite of LEFT JOIN (less commonly used)

```sql
SELECT u.name, o.order_id
FROM users u
RIGHT JOIN orders o
ON u.user_id = o.user_id;
```

---

#### 4️⃣ FULL OUTER JOIN

* Returns all rows from both tables

```sql
SELECT u.name, o.order_id
FROM users u
FULL OUTER JOIN orders o
ON u.user_id = o.user_id;
```

---

### ⚖️ Join Summary

| Join Type | Result              |
| --------- | ------------------- |
| INNER     | Only matches        |
| LEFT      | All left + matches  |
| RIGHT     | All right + matches |
| FULL      | All rows from both  |

---

### ⚙️ Real Example

**Problem:** Find all users and their orders (including users without orders)

```sql
SELECT u.name, o.order_id
FROM users u
LEFT JOIN orders o
ON u.user_id = o.user_id;
```

---

### ⚠️ Common Join Mistakes

* Missing join condition → **Cartesian product ❌**
* Using wrong join type
* Not handling NULL values

---

## 🧱 SUBQUERIES

### 🧠 What is a Subquery?

A **subquery** is a query nested inside another query.

---

### 🔄 Types of Subqueries

#### 1️⃣ Scalar Subquery

* Returns a single value

```sql
SELECT name
FROM users
WHERE age > (SELECT AVG(age) FROM users);
```

➡️ Users older than average

---

#### 2️⃣ Subquery in WHERE (Filtering)

```sql
SELECT name
FROM users
WHERE user_id IN (
    SELECT user_id FROM orders
);
```

➡️ Users who placed orders

---

#### 3️⃣ Subquery in FROM (Derived Table)

```sql
SELECT avg_age
FROM (
    SELECT AVG(age) AS avg_age FROM users
) t;
```

---

#### 4️⃣ Correlated Subquery

* Depends on outer query

```sql
SELECT u.name
FROM users u
WHERE EXISTS (
    SELECT 1 FROM orders o
    WHERE o.user_id = u.user_id
);
```

➡️ Evaluated row-by-row

---

## ⚔️ Joins vs Subqueries

| Aspect      | Joins                       | Subqueries                 |
| ----------- | --------------------------- | -------------------------- |
| Performance | Usually faster              | Can be slower              |
| Readability | Better for combining tables | Better for filtering logic |
| Use Case    | Merging datasets            | Nested conditions          |

➡️ In most cases, **JOIN is preferred for performance**

---

### 🔄 Example: Join vs Subquery

#### Using Subquery

```sql
SELECT name
FROM users
WHERE user_id IN (
    SELECT user_id FROM orders
);
```

#### Using Join (Preferred)

```sql
SELECT DISTINCT u.name
FROM users u
JOIN orders o
ON u.user_id = o.user_id;
```

---

### 🧠 Best Practices

#### 1️⃣ Prefer JOINs for Large Data

* More efficient in distributed systems

---

#### 2️⃣ Use Aliases

```sql
SELECT u.name
FROM users u;
```

➡️ Improves readability

---

#### 3️⃣ Avoid Nested Subqueries When Possible

* Harder to read and optimize

---

#### 4️⃣ Handle NULLs Carefully

* Especially in LEFT JOINs

---

### 🌍 Google-Level Thinking

At Google:

* Queries often involve:

  * Multiple joins across large datasets
* Poor join design can:

  * Explode data size
  * Increase cost significantly

➡️ Engineers focus on:

* Efficient joins
* Proper filtering before joining

---

### 🎯 Interview Insight

Interviewers expect you to:

* Understand all join types
* Know when to use:

  * JOIN vs subquery
* Avoid:

  * Cartesian joins
  * Inefficient nested queries

---

### ⚠️ Common Mistakes

* Forgetting join conditions
* Using subqueries where joins are better
* Not understanding NULL behavior
* Overcomplicating queries

---

### 🧠 Pro Tip

> Always ask:
> **“Am I combining data (JOIN) or filtering data (SUBQUERY)?”**

---

### ✅ Key Takeaways

* Joins combine data; subqueries filter or structure logic
* INNER and LEFT JOIN are most important
* Prefer JOINs for performance
* Understand correlated subqueries for advanced queries
* Mastery of joins is **critical for SQL interviews**

---
