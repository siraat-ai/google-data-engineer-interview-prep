## 4.4 Code Optimization Techniques

### 📌 Overview

**Code optimization** in Data Engineering is about making systems:

* Faster ⚡
* More memory-efficient 💾
* Cost-effective 💰

At companies like Google, inefficient code at scale can:

* Increase latency
* Crash systems
* Cost millions in compute

➡️ Optimization is not premature—it’s **essential at scale**

---

### 🧠 Optimization Mindset

> First make it work → Then make it correct → Then make it fast

Focus on:

* Bottlenecks
* Data size
* Execution patterns

---

### 🧱 Core Optimization Techniques

#### 1️⃣ Choose the Right Data Structures

* Use efficient structures for operations

```python
# ❌ Slow (O(n))
if x in my_list:

# ✅ Fast (O(1))
if x in my_set:
```

➡️ Data structures directly impact performance

---

#### 2️⃣ Avoid Unnecessary Loops

* Prefer vectorized or built-in operations

```python
# ❌ Inefficient
result = []
for x in data:
    result.append(x * 2)

# ✅ Optimized
result = [x * 2 for x in data]
```

---

#### 3️⃣ Minimize Data Movement

* Moving data is expensive

**Avoid:**

* Re-reading data multiple times
* Unnecessary data transfers between systems

➡️ Process data **close to where it lives**

---

#### 4️⃣ Use Lazy Evaluation

* Process data only when needed

**Example:**

* Generators instead of lists

```python
# ✅ Memory efficient
def generate_data():
    for i in range(10**9):
        yield i
```

---

#### 5️⃣ Optimize I/O Operations

* Disk and network I/O are slow

**Techniques:**

* Batch reads/writes
* Use efficient formats (Parquet over CSV)

---

#### 6️⃣ Parallelism & Concurrency

* Use multiple cores or machines

**Approaches:**

* Multithreading (I/O bound)
* Multiprocessing (CPU bound)
* Distributed systems (Spark, Dataflow)

➡️ Critical for large-scale data processing

---

#### 7️⃣ Caching Results

* Avoid recomputation

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def compute(x):
    return x * x
```

➡️ Useful for repeated computations

---

#### 8️⃣ Reduce Complexity (Big-O Thinking)

* Aim for efficient algorithms

| Complexity | Performance    |
| ---------- | -------------- |
| O(1)       | Best           |
| O(log n)   | Good           |
| O(n)       | Acceptable     |
| O(n²)      | Avoid at scale |

---

### 🔄 Before vs After Optimization

#### ❌ Inefficient

```python
def find_duplicates(data):
    duplicates = []
    for i in range(len(data)):
        for j in range(i + 1, len(data)):
            if data[i] == data[j]:
                duplicates.append(data[i])
    return duplicates
```

#### ✅ Optimized

```python
def find_duplicates(data):
    seen = set()
    duplicates = set()
    for item in data:
        if item in seen:
            duplicates.add(item)
        else:
            seen.add(item)
    return list(duplicates)
```

➡️ Reduced from **O(n²) → O(n)**

---

### ⚙️ Optimization in Data Pipelines

* Push computation to:

  * Data warehouses (e.g., SQL in BigQuery)
* Use:

  * Partitioning
  * Filtering early (predicate pushdown)

➡️ Process **less data whenever possible**

---

### 🌍 Google-Level Optimization Thinking

At Google:

* Engineers optimize for:

  * Latency (milliseconds matter)
  * Cost (large-scale compute)
* Techniques include:

  * Distributed processing
  * Efficient storage formats
  * Query optimization

➡️ Even small inefficiencies scale into **huge problems**

---

### ⚠️ Common Mistakes

* Optimizing too early without measurement
* Ignoring algorithm complexity
* Loading huge datasets into memory
* Overusing inefficient libraries (e.g., pandas for big data)
* Not leveraging distributed systems

---

### 🎯 Interview Insight

Interviewers expect:

* Awareness of:

  * Time/space complexity
* Ability to:

  * Improve naive solutions
  * Explain trade-offs

Strong candidates:

* Start simple
* Then optimize step-by-step

---

### 🧠 Pro Tip

> The best optimization is often **processing less data**, not faster code.

---

### ✅ Key Takeaways

* Optimization = **performance + efficiency + cost control**
* Focus on:

  * Data structures
  * Algorithm complexity
  * Data movement
* Use:

  * Parallelism
  * Caching
  * Efficient I/O
* Essential for:

  * Large-scale data systems
  * Big Tech engineering roles

---
