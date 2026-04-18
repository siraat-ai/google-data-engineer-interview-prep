## 5.1 Query Fundamentals

### 📌 Overview

**SQL Query Fundamentals** are the backbone of Data Engineering. Almost every data system—from pipelines to analytics—relies on efficient querying.

At companies like Google, strong SQL skills are:

* **Mandatory**
* Heavily tested in interviews
* Used daily in production systems

➡️ Mastering query fundamentals means understanding **how data is retrieved, filtered, and transformed efficiently**

---

### 🧠 What is a Query?

A **query** is a request to retrieve or manipulate data from a database.

```sql
SELECT name FROM users;
```

➡️ This retrieves the `name` column from the `users` table

---

### 🧱 Core SQL Clauses

#### 1️⃣ SELECT — Choose Columns

```sql
SELECT name, age FROM users;
```

* Specifies what data to retrieve

---

#### 2️⃣ FROM — Specify Table

```sql
SELECT * FROM users;
```

* Defines the data source

---

#### 3️⃣ WHERE — Filter Rows

```sql
SELECT * FROM users WHERE age > 18;
```

* Filters records based on conditions

---

#### 4️⃣ ORDER BY — Sort Results

```sql
SELECT * FROM users ORDER BY age DESC;
```

* Sorts data (ASC / DESC)

---

#### 5️⃣ LIMIT — Restrict Output

```sql
SELECT * FROM users LIMIT 10;
```

* Limits number of rows returned

---

### 🔄 SQL Query Execution Order (Important)

```text
FROM → WHERE → SELECT → ORDER BY → LIMIT
```

➡️ Understanding this helps avoid logical mistakes

---

### ⚙️ Basic Query Example

```sql
SELECT name, age
FROM users
WHERE age > 18
ORDER BY age DESC
LIMIT 5;
```

➡️ Returns top 5 oldest users above 18

---

### 🧱 Aggregation Basics

#### COUNT, SUM, AVG

```sql
SELECT COUNT(*) FROM users;
```

```sql
SELECT AVG(age) FROM users;
```

➡️ Used for summaries

---

### 🧱 GROUP BY — Aggregate by Category

```sql
SELECT country, COUNT(*)
FROM users
GROUP BY country;
```

➡️ Groups rows and applies aggregation

---

### 🧱 HAVING — Filter Aggregates

```sql
SELECT country, COUNT(*)
FROM users
GROUP BY country
HAVING COUNT(*) > 100;
```

➡️ Filters grouped results (after aggregation)

---

### 🧠 WHERE vs HAVING

| Clause | When Used          |
| ------ | ------------------ |
| WHERE  | Before aggregation |
| HAVING | After aggregation  |

---

### ⚙️ Real-World Example

**Problem:** Find top 3 countries with most users

```sql
SELECT country, COUNT(*) AS user_count
FROM users
GROUP BY country
ORDER BY user_count DESC
LIMIT 3;
```

➡️ Common interview-style query

---

### 🧠 Best Practices

#### 1️⃣ Avoid SELECT *

* Fetch only required columns
* Improves performance

---

#### 2️⃣ Filter Early

* Use WHERE to reduce data processed

---

#### 3️⃣ Use Aliases for Readability

```sql
SELECT COUNT(*) AS total_users FROM users;
```

---

#### 4️⃣ Write Clean Queries

* Proper formatting
* Clear structure

---

### ⚠️ Common Mistakes

* Misunderstanding execution order
* Using HAVING instead of WHERE unnecessarily
* Not grouping correctly
* Fetching too much data (`SELECT *`)

---

### 🌍 Google-Level Thinking

At Google:

* Queries run on **massive datasets (TB–PB)**
* Poor queries can:

  * Increase latency
  * Increase cost
* Engineers focus on:

  * Efficient filtering
  * Proper aggregation
  * Query optimization

---

### 🎯 Interview Insight

Interviewers expect:

* Strong understanding of:

  * SELECT, WHERE, GROUP BY, HAVING
* Ability to:

  * Write correct queries quickly
  * Handle edge cases
* Clean, readable SQL

---

### 🧠 Pro Tip

> SQL is not just about getting results—it’s about getting them **efficiently and correctly**

---

### ✅ Key Takeaways

* SQL fundamentals are **critical for Data Engineers**
* Master:

  * SELECT, WHERE, GROUP BY, HAVING
* Understand:

  * Execution order
  * Aggregations
* Write:

  * Efficient, readable queries
* This is one of the **most tested skills in interviews**

---
