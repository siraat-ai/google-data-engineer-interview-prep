## 4.1 Python for Data Engineering

### 📌 Overview

**Python** is the most widely used programming language in Data Engineering due to its:

* Simplicity
* Rich ecosystem
* Strong support for data processing

At companies like Google, Python is commonly used for:

* Data pipelines
* Automation
* Data transformation logic

➡️ It’s not about knowing Python syntax—it’s about using Python to build **scalable, production-ready systems**

---

### 🧠 Why Python for Data Engineering?

#### ✅ Key Advantages

* Easy to learn and read
* Massive ecosystem (data + cloud + ML)
* Strong community support
* Integrates well with distributed systems

---

### 🧱 Core Python Skills Required

#### 1️⃣ Data Structures

* Lists, Dictionaries, Sets, Tuples

```python
records = [{"user": 1}, {"user": 2}]
user_ids = [r["user"] for r in records]
```

➡️ Used for in-memory data manipulation

---

#### 2️⃣ File & Data Handling

* Read/write files (CSV, JSON, Parquet)

```python
import json

with open("data.json") as f:
    data = json.load(f)
```

---

#### 3️⃣ Functions & Modularity

* Write reusable, clean functions

```python
def clean_record(record):
    return record.strip().lower()
```

➡️ Improves maintainability

---

#### 4️⃣ Error Handling

* Handle failures gracefully

```python
try:
    process_data()
except Exception as e:
    print(f"Error: {e}")
```

➡️ Critical for production systems

---

#### 5️⃣ Working with APIs

* Fetch data from external systems

```python
import requests

response = requests.get("https://api.example.com/data")
data = response.json()
```

---

#### 6️⃣ Basic Object-Oriented Programming (OOP)

```python
class Pipeline:
    def run(self):
        print("Running pipeline")
```

➡️ Useful for structuring complex systems

---

### ⚙️ Key Python Libraries for Data Engineering

| Category               | Libraries           |
| ---------------------- | ------------------- |
| Data Processing        | pandas, numpy       |
| Distributed Processing | PySpark             |
| Workflow Orchestration | Airflow             |
| API & Networking       | requests            |
| Cloud Integration      | google-cloud-* SDKs |

---

### 🔄 Python in a Data Pipeline

```python
def pipeline():
    data = extract()
    cleaned = transform(data)
    load(cleaned)
```

➡️ Represents **ETL workflow in code**

---

### 🧠 Best Practices (Production-Level)

#### 1️⃣ Write Clean Code

* Use meaningful variable names
* Keep functions small

---

#### 2️⃣ Logging Instead of Print

```python
import logging
logging.info("Pipeline started")
```

---

#### 3️⃣ Handle Large Data Efficiently

* Avoid loading huge datasets into memory
* Use generators or distributed tools

---

#### 4️⃣ Use Virtual Environments

* Manage dependencies cleanly

---

#### 5️⃣ Write Testable Code

* Separate logic into functions
* Enable unit testing

---

### ⚠️ Common Mistakes

* Writing script-style code (not modular)
* Ignoring error handling
* Loading large datasets into memory
* Not using logging
* Overusing pandas for big data

---

### 🌍 Python at Scale (Google-Level Thinking)

At Google:

* Python is often used to:

  * Define pipeline logic
  * Glue systems together
* Heavy processing is handled by:

  * Distributed systems (e.g., Dataflow, Spark)

➡️ Python = **control layer**, not always the compute layer

---

### 🎯 Interview Insight

Interviewers expect:

* Clean, readable Python code
* Ability to:

  * Process data efficiently
  * Handle edge cases
* Understanding of:

  * Time/space complexity
  * Real-world constraints

---

### 🧩 Example: Simple ETL Pipeline

```python
def extract():
    return [" Apple ", "BANANA", None]

def transform(data):
    return [d.strip().lower() for d in data if d]

def load(data):
    print(data)

def run_pipeline():
    data = extract()
    cleaned = transform(data)
    load(cleaned)

run_pipeline()
```

---

### 🧠 Pro Tip

> Write Python like it will run **every day at scale**, not just once locally.

---

### ✅ Key Takeaways

* Python is the **primary language** for Data Engineering
* Focus on:

  * Clean, modular code
  * Error handling
  * Efficiency
* Use Python to:

  * Build pipelines
  * Integrate systems
* Combine Python with distributed tools for **large-scale processing**

---
