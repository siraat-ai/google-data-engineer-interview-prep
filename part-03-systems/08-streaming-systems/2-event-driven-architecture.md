## 8.2 Event-Driven Architecture

### 📌 Overview

**Event-Driven Architecture (EDA)** is a system design pattern where:

* Components communicate via **events**
* Systems react **asynchronously** to changes

At companies like Google, EDA is foundational for:

* Real-time data systems
* Scalable microservices
* Streaming pipelines

➡️ Instead of direct calls, systems communicate through **events**

---

## 🧠 Core Idea

> “Something happened” → Emit an event → Other systems react

---

## 🔄 High-Level Flow

```text id="6l2xq1"
[Producer]
   ↓ (event)
[Event Broker / Queue]
   ↓
[Consumers]
   ↓
[Actions / Processing]
```

---

## 🧱 Key Components

---

### 1️⃣ Event Producers

* Generate events when something happens

**Examples:**

* User clicks
* Payment completed
* Order placed

---

### 2️⃣ Event (Message)

* A record describing an action

```json
{
  "event_type": "order_created",
  "user_id": 123,
  "timestamp": "2025-01-01T10:00:00"
}
```

---

### 3️⃣ Event Broker (Message Queue)

* Routes events to consumers

**Examples:**

* Kafka
* Pub/Sub

➡️ Decouples producers and consumers

---

### 4️⃣ Event Consumers

* React to events

**Examples:**

* Update database
* Trigger ML model
* Send notification

---

## ⚙️ Example Flow

**E-commerce System:**

```text id="pr9v3j"
User places order
        ↓
Event: "order_created"
        ↓
Broker (Kafka / PubSub)
        ↓
Consumers:
   - Update inventory
   - Send email
   - Update analytics
```

➡️ One event → multiple independent actions

---

## 🧠 Key Characteristics

* **Asynchronous communication**
* **Loose coupling** (services independent)
* **Scalable & flexible**
* **Real-time responsiveness**

---

## ⚖️ Event-Driven vs Traditional Architecture

| Aspect        | Traditional (Request-Response) | Event-Driven |
| ------------- | ------------------------------ | ------------ |
| Communication | Direct calls                   | Events       |
| Coupling      | Tight                          | Loose        |
| Scalability   | Limited                        | High         |
| Flexibility   | Low                            | High         |

---

## 🧱 Event Patterns

---

### 1️⃣ Pub/Sub (Publish-Subscribe)

* Multiple consumers receive same event

---

### 2️⃣ Event Streaming

* Continuous flow of events

---

### 3️⃣ Event Sourcing

* Store events as source of truth

---

## 🧠 Benefits

* Scalable systems
* Independent services
* Real-time processing
* Easy to extend (add new consumers)

---

## ⚠️ Challenges

* Debugging complexity
* Event ordering issues
* Duplicate processing
* Managing state

---

## 🌍 Google-Level Perspective

At Google:

* Systems are highly event-driven:

  * User actions → events
  * Events → pipelines
* Tools:

  * Pub/Sub for messaging
  * Dataflow for processing

➡️ Enables:

* Real-time analytics
* Scalable distributed systems

---

## ⚙️ Example: Data Engineering Pipeline

```text id="cv3e1r"
User Click
   ↓
Event (click_event)
   ↓
Pub/Sub
   ↓
Dataflow
   ↓
BigQuery
```

➡️ Fully event-driven pipeline

---

## 🎯 Interview Insight

Interviewers expect:

* Understanding of:

  * Event-driven systems
  * Benefits vs trade-offs
* Ability to:

  * Design event-based pipelines

---

## ⚠️ Common Mistakes

* Tight coupling between services
* Ignoring event duplication
* Not handling failures
* Overcomplicating simple systems

---

## 🧠 Pro Tip

> Events should represent **facts**, not commands
> (“Order created” ✅ vs “Update inventory” ❌)

---

## ✅ Key Takeaways

* Event-Driven Architecture = **systems reacting to events**
* Core components:

  * Producers → Broker → Consumers
* Benefits:

  * Scalability
  * Flexibility
  * Real-time processing
* Challenges:

  * Complexity
  * Debugging
* Essential for:

  * Streaming systems
  * Modern data engineering architectures
