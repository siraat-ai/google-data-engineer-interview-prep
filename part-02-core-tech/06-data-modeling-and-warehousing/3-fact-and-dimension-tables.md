## 6.3 Fact & Dimension Tables

### 📌 Overview

**Fact and Dimension tables** are the core building blocks of **data warehouse design** (especially in star/snowflake schemas).

At companies like Google, they are used to:

* Structure analytical data
* Enable fast, scalable queries
* Support business intelligence and reporting

➡️ Understanding this is essential for **data modeling and system design interviews**

---

## 🧠 Core Idea

| Table Type          | Purpose                                 |
| ------------------- | --------------------------------------- |
| **Fact Table**      | Stores measurable events (metrics)      |
| **Dimension Table** | Stores descriptive attributes (context) |

---

## 🧱 Fact Table

### 📌 Definition

A **fact table** contains:

* **Quantitative data (metrics)**
* References to dimension tables (foreign keys)

---

### ⚙️ Example: Sales Fact Table

| sale_id | product_id | customer_id | date_id  | amount |
| ------- | ---------- | ----------- | -------- | ------ |
| 1       | 101        | 1001        | 20250101 | 200    |

---

### 🧠 Characteristics

* Large in size (millions–billions of rows)
* Numeric metrics:

  * Sales amount
  * Quantity
* Contains foreign keys to dimensions

---

### 📊 Types of Facts

| Type          | Description                                 |
| ------------- | ------------------------------------------- |
| Additive      | Can sum across all dimensions (e.g., sales) |
| Semi-additive | Limited aggregation (e.g., account balance) |
| Non-additive  | Cannot sum (e.g., ratios)                   |

---

## 🧱 Dimension Table

### 📌 Definition

A **dimension table** contains:

* Descriptive attributes that provide context to facts

---

### ⚙️ Example: Product Dimension

| product_id | product_name | category    | brand |
| ---------- | ------------ | ----------- | ----- |
| 101        | Laptop       | Electronics | Dell  |

---

### 🧠 Characteristics

* Smaller than fact tables
* Contains textual/descriptive data
* Used for filtering, grouping, labeling

---

## 🔄 Relationship Between Fact & Dimension

```text
Fact Table
   ↓ (foreign keys)
Dimension Tables
```

```text id="rfh0kz"
        [Customer Dim]
              |
[Product Dim]—[Sales Fact]—[Date Dim]
              |
        [Store Dim]
```

➡️ Fact table sits at the center (star schema)

---

## ⚙️ Example Query

**Problem:** Total sales by category

```sql
SELECT p.category, SUM(f.amount) AS total_sales
FROM sales f
JOIN product p ON f.product_id = p.product_id
GROUP BY p.category;
```

➡️ Fact provides metrics, dimension provides grouping

---

## 🧠 Key Differences

| Aspect    | Fact Table     | Dimension Table    |
| --------- | -------------- | ------------------ |
| Data Type | Numeric        | Descriptive        |
| Size      | Large          | Small              |
| Purpose   | Measure events | Provide context    |
| Keys      | Foreign keys   | Primary keys       |
| Usage     | Aggregation    | Filtering/grouping |

---

## 🧱 Types of Dimensions

* **Conformed Dimensions** → shared across tables
* **Slowly Changing Dimensions (SCD)** → track changes over time
* **Role-Playing Dimensions** → reused (e.g., order date, ship date)

---

## 🌍 Google-Level Perspective

At Google:

* Fact tables:

  * Store massive event data (clicks, impressions, logs)
* Dimension tables:

  * Store metadata (user info, product info)
* Systems like BigQuery:

  * Optimize queries over these structures

➡️ Proper modeling ensures:

* Fast queries
* Cost efficiency

---

## ⚠️ Common Mistakes

* Putting descriptive data in fact tables
* Not using proper keys
* Overloading dimension tables
* Ignoring data granularity

---

## 🎯 Interview Insight

Interviewers test:

* Ability to:

  * Identify fact vs dimension
  * Design schemas
* Understanding of:

  * Relationships
  * Query usage

---

## 🧠 Pro Tip

> Fact = **what happened**
> Dimension = **who, what, where, when, why**

---

## ✅ Key Takeaways

* Fact tables store **metrics/events**
* Dimension tables store **context/descriptions**
* Together they form the **foundation of data warehouses**
* Essential for:

  * Query performance
  * Scalable analytics
* Critical concept for **data modeling interviews**

---
