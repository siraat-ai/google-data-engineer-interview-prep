## 8.4 Exactly-Once vs At-Least-Once Processing

### 📌 Overview

In streaming systems, **delivery guarantees** define how reliably events are processed.

At companies like Google, choosing the right guarantee is critical for:

* Data correctness
* System reliability
* Cost and complexity

➡️ The two most important guarantees:

* **At-Least-Once**
* **Exactly-Once**

---

## 🧠 Core Idea

> What happens when failures occur during processing?

---

## 🔄 Processing Flow with Failures

```text id="8j7t9r"
Event → Process → Failure? → Retry → Result
```

➡️ The key question:

* Does the system process the event once, multiple times, or possibly miss it?

---

## 🧱 At-Least-Once Processing

### 📌 Definition

Each event is processed **one or more times**.

---

### 🧠 Behavior

* System retries on failure
* Ensures **no data loss**
* May cause **duplicate processing**

---

### ⚙️ Example

```text id="d6f1qe"
Event processed → Failure → Retry → Processed again
```

➡️ Same event processed twice

---

### ✅ Advantages

* Simple to implement
* Highly reliable (no data loss)

---

### ❌ Disadvantages

* Duplicate data possible
* Requires deduplication logic

---

### 🧠 When to Use

* Logging systems
* Analytics pipelines
* Non-critical duplicate handling

---

## 🧱 Exactly-Once Processing

### 📌 Definition

Each event is processed **exactly one time**—no duplicates, no loss.

---

### 🧠 Behavior

* Guarantees:

  * No duplicates
  * No missing events

---

### ⚙️ Example

```text id="b42j5m"
Event processed → Failure → System ensures no duplicate processing
```

---

### ✅ Advantages

* Perfect data accuracy
* No deduplication needed

---

### ❌ Disadvantages

* Complex to implement
* Higher cost
* Performance overhead

---

### 🧠 When to Use

* Financial transactions
* Billing systems
* Critical business logic

---

## ⚖️ At-Least-Once vs Exactly-Once

| Aspect      | At-Least-Once | Exactly-Once |
| ----------- | ------------- | ------------ |
| Data Loss   | No            | No           |
| Duplicates  | Possible      | No           |
| Complexity  | Low           | High         |
| Performance | Faster        | Slower       |
| Cost        | Lower         | Higher       |

---

## 🧠 Key Concept: Idempotency

> The most practical solution for duplicates

### 📌 Definition

An operation is **idempotent** if:

* Running it multiple times → same result

---

### ⚙️ Example

```python
# Idempotent insert
INSERT INTO table (id, value)
ON CONFLICT (id) DO NOTHING;
```

➡️ Prevents duplicates even with retries

---

## 🔄 Real-World Strategy

In practice:

```text id="d1k3qe"
At-Least-Once + Idempotency = Effectively Exactly-Once
```

➡️ This is widely used in production systems

---

## 🌍 Google-Level Perspective

At Google:

* Systems often use:

  * At-least-once delivery
  * Idempotent processing
* Tools like Dataflow provide:

  * Exactly-once semantics (under the hood)

➡️ Balance between:

* Performance
* Complexity
* Reliability

---

## ⚠️ Common Mistakes

* Assuming exactly-once is always needed
* Not handling duplicates
* Ignoring idempotency
* Overcomplicating systems

---

## 🎯 Interview Insight

Interviewers expect:

* Understanding of:

  * Trade-offs
  * Failure scenarios
* Ability to:

  * Design systems with correct guarantees

Strong answer:

* “Use at-least-once with idempotency for scalability”

---

## 🧠 Pro Tip

> Exactly-once is expensive—
> simulate it with **idempotent design whenever possible**

---

## ✅ Key Takeaways

* At-least-once:

  * Reliable but may duplicate
* Exactly-once:

  * Accurate but complex
* Idempotency is the key to handling duplicates
* Most real systems use:

  * **At-least-once + deduplication**
* Critical concept for:

  * Streaming systems
  * System design interviews
