## 6.5 Slowly Changing Dimensions (SCD)

### 📌 Overview

**Slowly Changing Dimensions (SCD)** refer to techniques used to manage **changes in dimension data over time**.

At companies like Google, SCD is critical for:

* Maintaining **historical accuracy**
* Supporting **time-based analytics**
* Enabling **correct reporting**

➡️ Real-world data changes (addresses, prices, categories), and we must decide **how to handle those changes**

---

## 🧠 The Problem

**Example:**

* A customer moves to a new city

Question:

> Do we overwrite the old data or keep history?

➡️ This decision defines the **SCD type**

---

## 🧱 SCD Types

---

### 1️⃣ Type 0 — No Change

* Data is never updated

```text
Original Value → Always stays the same
```

✅ Use case:

* Static data (e.g., date of birth)

---

### 2️⃣ Type 1 — Overwrite

* Old data is replaced with new data

```text
Old Value → New Value (no history)
```

**Example:**

| customer_id | city             |
| ----------- | ---------------- |
| 1           | Berlin → Hamburg |

---

#### ✅ Advantages

* Simple
* No extra storage

#### ❌ Disadvantages

* No historical tracking

---

### 3️⃣ Type 2 — Add New Row (Most Important)

* Preserve history by adding new rows

```text
Old Record → New Record (with timestamps)
```

---

#### ⚙️ Example

| customer_id | city    | start_date | end_date |
| ----------- | ------- | ---------- | -------- |
| 1           | Berlin  | 2020       | 2023     |
| 1           | Hamburg | 2023       | NULL     |

---

#### 🧠 Key Features

* Multiple records per entity
* Tracks full history
* Uses:

  * `start_date`
  * `end_date`
  * `is_current` flag

---

#### ✅ Advantages

* Full historical tracking
* Accurate time-based analysis

#### ❌ Disadvantages

* More storage
* More complex queries

---

### 4️⃣ Type 3 — Add New Column

* Store limited history in new columns

```text
city → current_city, previous_city
```

---

#### ⚙️ Example

| customer_id | current_city | previous_city |
| ----------- | ------------ | ------------- |
| 1           | Hamburg      | Berlin        |

---

#### ✅ Advantages

* Simple history tracking

#### ❌ Disadvantages

* Limited history (only last value)

---

## ⚖️ SCD Comparison

| Type   | History | Complexity | Use Case              |
| ------ | ------- | ---------- | --------------------- |
| Type 0 | None    | Low        | Static data           |
| Type 1 | No      | Low        | Latest value only     |
| Type 2 | Full    | High       | Analytics & reporting |
| Type 3 | Limited | Medium     | Recent changes        |

---

## 🔄 Real-World Example

**E-commerce: Product Price Changes**

* Type 1:

  * Only current price stored
* Type 2:

  * Track price over time → enables:

    * Historical revenue analysis

---

## 🧠 Why SCD Matters

Without SCD:

* Historical reports become incorrect
* Trends cannot be analyzed properly

➡️ Example:

* “What was revenue when product price was $100?”

---

## ⚙️ Example Query (Type 2)

**Get current customer records**

```sql
SELECT *
FROM customers
WHERE end_date IS NULL;
```

---

**Get historical data**

```sql
SELECT *
FROM customers
WHERE customer_id = 1;
```

---

## 🌍 Google-Level Perspective

At Google:

* Type 2 SCD is widely used for:

  * User data changes
  * Product attributes
  * Feature tracking
* Enables:

  * Accurate ML training data
  * Time-based analytics

➡️ Historical correctness is critical at scale

---

## ⚠️ Common Mistakes

* Using Type 1 when history is needed
* Not tracking timestamps
* Poor handling of “current” records
* Overcomplicating when history isn’t required

---

## 🎯 Interview Insight

Interviewers expect:

* Understanding of:

  * Different SCD types
* Ability to:

  * Choose appropriate type
  * Explain trade-offs

---

## 🧠 Pro Tip

> If your analysis depends on **time**, you likely need **Type 2 SCD**

---

## ✅ Key Takeaways

* SCD handles **changes in dimension data over time**
* Types:

  * Type 1 → overwrite
  * Type 2 → full history (most important)
  * Type 3 → limited history
* Critical for:

  * Accurate analytics
  * Historical reporting
* One of the most important concepts in **data warehousing**

---
