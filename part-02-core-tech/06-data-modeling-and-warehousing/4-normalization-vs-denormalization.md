## 6.4 Data Normalization vs Denormalization

### 📌 Overview

**Normalization** and **Denormalization** are two opposite approaches to structuring data in databases.

At companies like Google, choosing between them depends on:

* System type (OLTP vs OLAP)
* Performance requirements
* Data consistency needs

➡️ This is a **core data modeling concept** and frequently tested in interviews

---

## 🧠 Core Idea

| Approach            | Goal                                    |
| ------------------- | --------------------------------------- |
| **Normalization**   | Reduce redundancy & improve consistency |
| **Denormalization** | Improve read performance                |

---

## 🧱 Normalization

### 📌 Definition

Organizing data into **multiple related tables** to:

* Eliminate redundancy
* Ensure data integrity

---

### ⚙️ Example (Normalized)

**Users Table**

| user_id | name  |
| ------- | ----- |
| 1       | Alice |

**Orders Table**

| order_id | user_id |
| -------- | ------- |
| 101      | 1       |

➡️ Data is split across tables

---

### 🧠 Characteristics

* Minimal data duplication
* Uses foreign keys
* Requires joins to query

---

### ✅ Advantages

* Data consistency
* Easier updates
* Reduced storage

---

### ❌ Disadvantages

* More joins → slower queries
* Complex queries

---

## 🧱 Denormalization

### 📌 Definition

Combining data into **fewer tables** to:

* Reduce joins
* Improve query performance

---

### ⚙️ Example (Denormalized)

| order_id | user_id | user_name |
| -------- | ------- | --------- |
| 101      | 1       | Alice     |

➡️ Data duplication exists

---

### 🧠 Characteristics

* Redundant data
* Fewer joins
* Faster reads

---

### ✅ Advantages

* Faster queries
* Simpler queries
* Better for analytics

---

### ❌ Disadvantages

* Data duplication
* Update anomalies
* More storage usage

---

## ⚖️ Normalization vs Denormalization

| Aspect      | Normalization     | Denormalization       |
| ----------- | ----------------- | --------------------- |
| Redundancy  | Low               | High                  |
| Performance | Slower reads      | Faster reads          |
| Complexity  | High (joins)      | Low                   |
| Storage     | Efficient         | More usage            |
| Updates     | Easy & consistent | Risk of inconsistency |

---

## 🔄 When to Use Each

### 🟢 Use Normalization (OLTP Systems)

* Transactional systems
* Frequent updates
* Data consistency critical

**Examples:**

* Banking
* User management

---

### 🔵 Use Denormalization (OLAP Systems)

* Analytics & reporting
* Large-scale queries
* Read-heavy workloads

**Examples:**

* Data warehouses
* Dashboards

---

## 🌍 Google-Level Perspective

At Google:

* **OLTP systems**

  * Use normalized schemas
  * Ensure data integrity

* **OLAP systems (e.g., BigQuery)**

  * Use denormalized schemas
  * Optimize for fast queries

➡️ Data Engineers often:

* Extract normalized data
* Transform it into denormalized formats for analytics

---

## ⚙️ Real-World Example

**E-commerce System:**

* OLTP:

  * Separate tables (users, orders, products)
* OLAP:

  * Combined table for analytics

➡️ Trade-off:

* Consistency vs performance

---

## ⚠️ Common Mistakes

* Over-normalizing analytics systems
* Over-denormalizing transactional systems
* Ignoring workload requirements
* Not considering query patterns

---

## 🎯 Interview Insight

Interviewers expect:

* Clear understanding of:

  * Trade-offs
  * Use cases
* Ability to:

  * Choose appropriate design
  * Explain reasoning

---

## 🧠 Pro Tip

> Normalize for **writes & consistency**
> Denormalize for **reads & performance**

---

## ✅ Key Takeaways

* Normalization reduces redundancy and improves integrity
* Denormalization improves query performance
* Use:

  * Normalization → OLTP
  * Denormalization → OLAP
* Trade-offs are critical—there’s no one-size-fits-all
* Essential concept for **data modeling and system design interviews**

---
