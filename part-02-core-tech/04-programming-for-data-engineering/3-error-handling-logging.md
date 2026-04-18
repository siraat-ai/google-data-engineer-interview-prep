## 4.3 Error Handling & Logging

### 📌 Overview

In Data Engineering, failures are **inevitable**—APIs fail, data is malformed, systems crash.

At companies like Google, the expectation is:

> Systems should **fail gracefully, recover automatically, and be easy to debug**

➡️ This is achieved through **robust error handling + structured logging**

---

### 🧠 Why It Matters

Without proper error handling & logging:

* Pipelines fail silently ❌
* Debugging becomes impossible ❌
* Data quality issues go unnoticed ❌

With it:

* Failures are **visible, traceable, and recoverable** ✅

---

### 🧱 Error Handling Fundamentals

#### 1️⃣ Never Assume Success

* External systems can fail:

  * APIs
  * Databases
  * File systems

```python id="3h7n0r"
def fetch_data():
    raise Exception("API failed")
```

➡️ Always prepare for failure

---

#### 2️⃣ Use Try-Except Blocks

```python id="u4o2l9"
try:
    data = fetch_data()
except Exception as e:
    print(f"Error: {e}")
```

➡️ Prevents crashes and allows controlled handling

---

#### 3️⃣ Handle Specific Exceptions

```python id="d5qnt6"
try:
    value = int("abc")
except ValueError:
    print("Invalid number format")
```

➡️ More precise and safer than generic exceptions

---

#### 4️⃣ Fail Fast vs Fail Gracefully

| Strategy        | When to Use                           |
| --------------- | ------------------------------------- |
| Fail Fast       | Critical errors (stop pipeline)       |
| Fail Gracefully | Non-critical errors (skip & continue) |

---

#### 5️⃣ Retry Mechanisms 🔁

* Temporary failures should be retried

```python id="p0d3mr"
import time

for _ in range(3):
    try:
        fetch_data()
        break
    except Exception:
        time.sleep(2)
```

➡️ Common in network/API failures

---

#### 6️⃣ Idempotency

* Ensure retries don’t cause:

  * Duplicate data
  * Corruption

➡️ Critical for safe recovery

---

### 🧱 Logging Fundamentals

#### 1️⃣ Use Logging (Not Print)

```python id="2y4l3t"
import logging

logging.basicConfig(level=logging.INFO)
logging.info("Pipeline started")
```

---

#### 2️⃣ Log Levels

| Level    | Purpose                  |
| -------- | ------------------------ |
| DEBUG    | Detailed debugging info  |
| INFO     | General events           |
| WARNING  | Unexpected but non-fatal |
| ERROR    | Failures                 |
| CRITICAL | System-breaking issues   |

```python id="xv6w2m"
logging.error("Failed to load data")
```

---

#### 3️⃣ Structured Logging

* Include context:

```python id="dlxq6g"
logging.info("Processed record", extra={"user_id": 123})
```

➡️ Makes logs searchable and useful

---

#### 4️⃣ Log Important Events Only

Log:

* Pipeline start/end
* Errors
* Key transformations

Avoid:

* Excessive noise

---

### 🔄 Example: Production-Ready Pipeline

```python id="k8z0sy"
import logging

logging.basicConfig(level=logging.INFO)

def run_pipeline():
    try:
        logging.info("Pipeline started")
        data = extract()
        cleaned = transform(data)
        load(cleaned)
        logging.info("Pipeline completed successfully")
    except Exception as e:
        logging.error(f"Pipeline failed: {e}")
        raise
```

---

### ⚙️ Error Handling + Logging Together

```text id="u9jz4p"
Error occurs
     ↓
Catch exception
     ↓
Log error with context
     ↓
Retry or fail safely
```

➡️ This flow ensures **visibility + recovery**

---

### 🌍 Google-Level Practices

At Google:

* Systems are designed to:

  * Automatically retry failures
  * Log detailed events
  * Integrate with monitoring tools
* Engineers rely on logs to:

  * Debug production issues
  * Perform root cause analysis

➡️ Logging is treated as a **first-class feature**

---

### ⚠️ Common Mistakes

* Using `print()` instead of logging
* Catching exceptions without logging
* Ignoring retries
* Over-logging (noise)
* Not including context in logs

---

### 🎯 Interview Insight

Interviewers look for:

* Awareness of failure scenarios
* Proper use of:

  * Try/except
  * Logging
* Ability to design **resilient systems**

---

### 🧠 Pro Tip

> If your system fails and you don’t know why,
> your logging strategy has already failed.

---

### ✅ Key Takeaways

* Failures are **expected**—design for them
* Error handling ensures:

  * Stability
  * Recovery
* Logging ensures:

  * Visibility
  * Debuggability
* Together, they are essential for:

  * **Production-grade data systems**

---
