## 6.2 Star Schema vs Snowflake Schema

### 📌 Overview

**Star Schema** and **Snowflake Schema** are two fundamental data modeling approaches used in **OLAP systems (data warehouses)**.

At companies like Google, choosing the right schema impacts:

* Query performance
* Storage efficiency
* Maintainability

➡️ This is a **frequently tested interview topic**

---

## 🧠 Core Idea

| Schema               | Philosophy                |
| -------------------- | ------------------------- |
| **Star Schema**      | Simplicity & performance  |
| **Snowflake Schema** | Normalization & structure |

---

## ⭐ Star Schema

### 📌 Definition

A **denormalized** schema where:

* A central **fact table** connects directly to **dimension tables**

---

### 🧱 Structure

```text
        [Dimension]
            |
[Dimension]—[Fact Table]—[Dimension]
            |
        [Dimension]
```

---

### ⚙️ Example

* **Fact Table:** `sales`
* **Dimensions:**

  * `customer`
  * `product`
  * `date`

```sql
SELECT d.year, SUM(f.sales_amount)
FROM sales f
JOIN date d ON f.date_id = d.date_id
GROUP BY d.year;
```

---

### ✅ Advantages

* Simple design
* Faster queries (fewer joins)
* Easy to understand

---

### ❌ Disadvantages

* Data redundancy
* Larger storage usage

---

## ❄️ Snowflake Schema

### 📌 Definition

A **normalized** version of star schema where:

* Dimension tables are split into **multiple related tables**

---

### 🧱 Structure

```text
          [Sub-Dimension]
                |
[Dimension]—[Fact Table]—[Dimension]
                |
          [Sub-Dimension]
```

---

### ⚙️ Example

* `product` → split into:

  * product
  * category
  * brand

```sql
SELECT c.category_name, SUM(f.sales_amount)
FROM sales f
JOIN product p ON f.product_id = p.product_id
JOIN category c ON p.category_id = c.category_id
GROUP BY c.category_name;
```

---

### ✅ Advantages

* Reduced data redundancy
* Better data integrity
* Easier updates

---

### ❌ Disadvantages

* More joins → slower queries
* More complex design

---

## ⚖️ Star vs Snowflake Comparison

| Aspect            | Star Schema          | Snowflake Schema    |
| ----------------- | -------------------- | ------------------- |
| Design            | Denormalized         | Normalized          |
| Query Performance | Faster               | Slower (more joins) |
| Storage           | Higher               | Lower               |
| Complexity        | Simple               | Complex             |
| Maintenance       | Harder (duplication) | Easier              |

---

## 🔄 When to Use Each

### ⭐ Use Star Schema When:

* Query performance is critical
* Simpler analytics use cases
* Large-scale reporting

---

### ❄️ Use Snowflake Schema When:

* Data consistency is critical
* Complex hierarchical relationships
* Storage optimization matters

---

## 🌍 Google-Level Perspective

At Google:

* Data warehouses (e.g., BigQuery) often favor:

  * **Star schema-like designs**
* Why?

  * Fewer joins → faster queries at scale
  * Compute is cheaper than complexity

➡️ Performance usually outweighs normalization in analytics systems

---

## 🧠 Real-World Example

**E-commerce Analytics**

* Star Schema:

  * One `product` table with all attributes
* Snowflake Schema:

  * Separate tables for:

    * product
    * category
    * supplier

➡️ Trade-off: simplicity vs structure

---

## ⚠️ Common Mistakes

* Over-normalizing OLAP schemas
* Using snowflake when not needed
* Ignoring query performance
* Not understanding trade-offs

---

## 🎯 Interview Insight

Interviewers expect:

* Clear explanation of:

  * Differences
  * Trade-offs
* Ability to:

  * Choose schema based on use case

Strong answer:

* “Star schema for performance, snowflake for normalization”

---

## 🧠 Pro Tip

> In analytics systems, **fewer joins = better performance**

---

## ✅ Key Takeaways

* Star schema = **simple, fast, denormalized**
* Snowflake schema = **normalized, structured, complex**
* Trade-off:

  * Performance vs storage & integrity
* Star schema is more common in modern data warehouses
* Critical concept for **data modeling interviews**

---
