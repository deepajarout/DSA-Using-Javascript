# 💬 Chat System Design (WhatsApp-like) — Detailed

---

## 📌 1. Problem Statement

Design a scalable **real-time chat system** where users can:
- Send/receive messages instantly
- See online/offline status
- Support 1-1 and group chat
- Get message delivery & read receipts

---

## 📌 2. Requirements

### ✅ Functional Requirements
- 1-1 messaging
- Group messaging
- Message delivery (real-time)
- Message status (sent, delivered, read)
- Media sharing (images, videos)
- Online/offline presence

---

### ⚡ Non-Functional Requirements
- Low latency (<200ms)
- High availability
- Scalable to millions of users
- Reliable message delivery (no loss)

---

## 📌 3. High-Level Architecture

```
Client (Mobile/Web)
        ↓
   Load Balancer
        ↓
   WebSocket Server
        ↓
-----------------------------------
| Chat Service   | Presence Service |
| Message Queue  | Media Service    |
-----------------------------------
        ↓
     Database (NoSQL)
        ↓
     Cache (Redis)
```

---

## 📌 4. Core Components

### 1. WebSocket Server
- Maintains persistent connections
- Enables real-time communication

---

### 2. Chat Service
- Handles message sending/receiving
- Business logic for chats

---

### 3. Presence Service
- Tracks user online/offline status
- Uses Redis (fast access)

---

### 4. Message Queue (Kafka)
- Buffers messages
- Ensures reliability
- Handles spikes

---

### 5. Media Service
- Upload/download images/videos
- Uses object storage (S3)

---

### 6. Database (NoSQL - Cassandra/MongoDB)
- Stores messages
- Optimized for high writes

---

## 📌 5. Message Flow (Step-by-Step)

### 📤 Sending Message

1. User A sends message
2. Message goes via WebSocket
3. Backend validates message
4. Message pushed to Queue (Kafka)
5. Stored in DB
6. Delivered to User B if online
7. If offline → stored for later delivery

---

### 📥 Receiving Message

1. User B is online → gets message instantly
2. If offline → receives on next login
3. Message status updated:
   - Sent ✅
   - Delivered 📩
   - Read 👀

---

## 📌 6. Real-Time Delivery

- Use **WebSockets** (NOT HTTP polling)
- Maintain persistent connection
- Push messages instantly

---

## 📌 7. Database Design

### Messages Table

```
message_id
sender_id
receiver_id / group_id
content
timestamp
status
```

---

### Conversations Table

```
conversation_id
participants
last_message
```

---

## 📌 8. Scaling Strategies

### 🔥 Horizontal Scaling
- Multiple WebSocket servers
- Load balancer distributes traffic

---

### 🔥 Partitioning
- Partition messages by:
  - user_id OR conversation_id

---

### 🔥 Caching
- Redis for:
  - Online users
  - Recent chats

---

### 🔥 Message Queue
- Kafka for:
  - Async processing
  - Reliability

---

## 📌 9. Handling Offline Users

- Store messages in DB
- Deliver when user reconnects
- Use push notifications

---

## 📌 10. Group Chat Design

- Store group_id instead of receiver_id
- Fan-out strategies:
  - **Fan-out on write** (store for each user)
  - **Fan-out on read** (compute on demand)

---

## 📌 11. Failure Handling

- Retry failed messages
- Use Dead Letter Queue
- Acknowledge message delivery

---

## 📌 12. Bottlenecks & Solutions

| Problem | Solution |
|--------|---------|
| High connections | WebSocket scaling |
| Message loss | Queue (Kafka) |
| DB overload | Partitioning |
| Offline delivery | Store & forward |

---

## 📌 13. APIs (Fallback for HTTP)

### Send Message
```
POST /messages
```

### Get Messages
```
GET /messages/{conversation_id}
```

---

## 📌 14. Advanced Features (Impress Interviewer)

- Typing indicator
- End-to-end encryption
- Message reactions
- Message edit/delete
- Push notifications

---

## 🎯 Interview Tips

- Say: “I will use WebSockets for real-time communication”
- Say: “Kafka ensures message durability”
- Mention: “Redis for presence tracking”

---

## 🚀 One-Line Summary

> A scalable real-time chat system using WebSockets, Kafka, Redis, and NoSQL DB to ensure low latency and high reliability.
