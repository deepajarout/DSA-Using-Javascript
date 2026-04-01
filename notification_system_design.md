# 🧠 System Design: Notification System

---

## 📌 Problem Statement

Design a scalable notification system that can send:

* Email 📧
* SMS 📱
* Push Notifications 🔔

Used by applications like Facebook, Amazon, Netflix.

---

## 🎯 Requirements

### ✅ Functional Requirements

* Send notifications to users
* Support multiple channels (Email, SMS, Push)
* Retry failed notifications
* Schedule notifications for later

### 🚀 Non-Functional Requirements

* High scalability (millions of users)
* Low latency
* High availability
* Fault tolerance

---

## 🏗️ High-Level Design (HLD)

```
Client → API Gateway → Notification Service → Message Queue → Workers → External Services
```

---

## 🔹 Components

### 1. API Gateway

* Entry point for all requests
* Handles authentication and rate limiting

---

### 2. Notification Service

* Processes incoming requests
* Decides:

  * Notification type
  * Priority
* Pushes message to queue

---

### 3. Message Queue

* Example: Kafka / RabbitMQ
* Decouples system
* Handles traffic spikes

---

### 4. Workers (Consumers)

* Consume messages from queue
* Send notifications via external services

---

### 5. External Services

* Email Service (e.g., SendGrid)
* SMS Service (e.g., Twilio)
* Push Notification Service (e.g., Firebase)

---

## 🧩 Low-Level Design (LLD)

### 📦 Notification Object

```json
{
  "userId": "123",
  "type": "EMAIL",
  "message": "Welcome!",
  "status": "PENDING",
  "retryCount": 0,
  "scheduledAt": "timestamp"
}
```

---

## 🔁 Retry Mechanism

* Retry up to 3 times
* Use exponential backoff
* If still failing → move to Dead Letter Queue (DLQ)

---

## ⚙️ Database Design

### Users Table

```
user_id | email | phone | device_token
```

### Notifications Table

```
id | user_id | type | status | retry_count | created_at
```

---

## 🚀 Scaling Strategy

### Horizontal Scaling

* Add more worker instances

### Queue Partitioning

* Partition based on userId

### Load Handling

* Queue absorbs traffic spikes

---

## ❗ Bottlenecks & Solutions

| Problem            | Solution         |
| ------------------ | ---------------- |
| High traffic       | Rate limiting    |
| Failed delivery    | Retry + DLQ      |
| Slow external APIs | Async processing |
| Duplicate messages | Idempotency      |

---

## 🧠 Key Interview Points

* Use queue-based architecture
* System is event-driven
* Retry mechanism ensures reliability
* Workers scale horizontally
* External services handle delivery

---

## 🎯 Advanced Enhancements

* Priority queue (urgent vs normal)
* Batch notifications
* User preferences (mute/opt-out)
* Analytics (delivery rate, open rate)

---

## 🏁 Summary

* Use async architecture (Queue + Workers)
* Ensure scalability
