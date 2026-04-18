## 6.1 OLTP vs OLAP

### 📌 Overview

**OLTP (Online Transaction Processing)** and **OLAP (Online Analytical Processing)** are two fundamental types of data systems used for **different workloads**.

At companies like Google, both systems coexist:

* OLTP → powers **real-time applications**
* OLAP → powers **analytics and decision-making**

➡️ Understanding the difference is critical for **data modeling, system design, and interviews**

---

### 🧠 Core Idea

| System   | Purpose                       |
| -------- | ----------------------------- |
| **OLTP** | Handle real-time transactions |
| **OLAP** | Analyze large volumes of data |

---

### 🔄 High-Level Architecture

```text
[Users / Apps]
      ↓
   OLTP System  → (Operational Data)
      ↓
   ETL / ELT Pipeline
      ↓
   OLAP System  → (Analytics / Reporting)
```

---

## 🧱 OLTP (Online Transaction Processing)

### 📌 Definition

Systems designed to handle **high volumes of small, fast transactions**.

---

### ⚙️ Characteristics

* Real-time operations
* High concurrency (many users)
* Small, frequent queries
* Strong consistency (ACID)

---

### 🧾 Example Queries

```sql
INSERT INTO orders VALUES (...);
SELECT * FROM users WHERE user_id = 123;
```

---

### 🏗️ Examples

* Banking systems
* E-commerce checkout
* User authentication systems

---

### 🧠 Design Focus

* Fast writes & reads
* Data integrity
* Normalized schemas

---

## 🧱 OLAP (Online Analytical Processing)

### 📌 Definition

Systems designed for **complex queries and large-scale data analysis**.

---

### ⚙️ Characteristics

* Large data scans (TB–PB)
* Complex queries (aggregations, joins)
* Read-heavy workloads
* Optimized for analytics

---

### 🧾 Example Queries

```sql
SELECT country, COUNT(*)
FROM users
GROUP BY country;
```

---

### 🏗️ Examples

* Business dashboards
* Data warehouses (e.g., BigQuery)
* Reporting systems

---

### 🧠 Design Focus

* Fast query performance
* Denormalized schemas
* Columnar storage

---

## ⚖️ OLTP vs OLAP Comparison

| Aspect            | OLTP                 | OLAP               |
| ----------------- | -------------------- | ------------------ |
| Purpose           | Transactions         | Analytics          |
| Query Type        | Simple               | Complex            |
| Data Size         | Small                | Large              |
| Operations        | Insert/Update/Delete | Read-heavy         |
| Schema            | Normalized           | Denormalized       |
| Performance Focus | Low latency          | High throughput    |
| Users             | End-users/apps       | Analysts/engineers |

---

### 🔄 Real-World Example

**E-commerce System:**

* **OLTP**

  * User places an order
  * Payment processed instantly

* **OLAP**

  * Analyze:

    * Daily sales
    * Top products
    * User behavior

---

### 🌍 Google-Level Perspective

At Google:

* **OLTP Systems**

  * Handle:

    * Search queries
    * User interactions
* **OLAP Systems**

  * Use tools like:

    * BigQuery
  * Analyze:

    * Logs
    * User behavior
    * Ad performance

➡️ Data flows from OLTP → OLAP via pipelines

---

### 🧠 Why This Matters for Data Engineers

* You design pipelines that:

  * Extract data from OLTP
  * Transform it
  * Load into OLAP systems

➡️ You bridge **operational systems and analytics systems**

---

### ⚠️ Common Mistakes

* Using OLTP systems for analytics (slow ❌)
* Over-normalizing OLAP schemas
* Ignoring workload differences

---

### 🎯 Interview Insight

Interviewers test:

* Understanding of:

  * System differences
  * When to use each
* Ability to:

  * Design pipelines between them

---

### 🧠 Pro Tip

> OLTP = “Run the business”
> OLAP = “Understand the business”

---

### ✅ Key Takeaways

* OLTP handles **real-time transactions**
* OLAP handles **large-scale analytics**
* Key differences:

  * Workload
  * Query complexity
  * Data modeling
* Data Engineers connect OLTP → OLAP via pipelines
* Essential concept for **system design interviews**

---
