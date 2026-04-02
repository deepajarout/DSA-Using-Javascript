# 🍔 Food Delivery System Design (Swiggy-like)

## 📌 1. Problem Statement

Design a scalable **Food Delivery System** where users can:
- Browse restaurants
- Place orders
- Track delivery in real-time

---

## 📌 2. Requirements

### ✅ Functional Requirements
- User can search restaurants
- View menu
- Place order
- Make payment
- Track order
- Delivery partner assignment

### ⚡ Non-Functional Requirements
- High availability
- Low latency
- Scalable system
- Real-time tracking

---

## 📌 3. High-Level Architecture

```
Client (Web/Mobile)
        ↓
   API Gateway
        ↓
---------------------------------------
| User Service        | Order Service  |
| Restaurant Service  | Payment Service|
| Delivery Service    | Tracking Service|
---------------------------------------
        ↓
     Database
        ↓
     Cache (Redis)
        ↓
 Message Queue (Kafka)
```

---

## 📌 4. Core Components

### 1. User Service
- Manages user profiles
- Authentication & authorization

### 2. Restaurant Service
- Stores restaurant data
- Menu management
- Availability status

### 3. Order Service
- Handles order creation
- Updates order status

### 4. Payment Service
- Handles transactions
- Integrates with payment gateways

### 5. Delivery Service
- Assigns delivery partners
- Tracks delivery status

### 6. Tracking Service
- Real-time location tracking
- Uses GPS/WebSockets

---

## 📌 5. Data Flow

### 🛒 Order Placement Flow

1. User selects food items
2. Sends request to Order Service
3. Order stored in DB
4. Event sent to Queue (Kafka)
5. Restaurant gets notified
6. Delivery partner assigned
7. Payment processed
8. Order confirmed

---

### 🚴 Delivery Flow

1. Delivery partner accepts order
2. Location updates sent continuously
3. Tracking Service updates user UI
4. Order marked delivered

---

## 📌 6. Database Design

### 🧾 Tables

#### Users
```
user_id, name, email, address
```

#### Restaurants
```
restaurant_id, name, location, rating
```

#### Menu
```
item_id, restaurant_id, price
```

#### Orders
```
order_id, user_id, status, total_price
```

#### Delivery
```
delivery_id, order_id, partner_id, status
```

---

## 📌 7. Scaling Strategies

### 🔥 1. Caching
- Use Redis for:
  - Restaurant list
  - Menu data

### 🔥 2. Load Balancing
- Distribute traffic across servers

### 🔥 3. Database Sharding
- Split data by:
  - Location (city-based)

### 🔥 4. Message Queue
- Kafka for:
  - Order processing
  - Notifications

### 🔥 5. CDN
- Serve images (menu, restaurant)

---

## 📌 8. Real-Time Tracking

- Use WebSockets
- Delivery partner sends GPS updates
- Backend pushes updates to user

---

## 📌 9. Failure Handling

- Retry failed payments
- Dead Letter Queue for failed events
- Fallback for delivery reassignment

---

## 📌 10. Bottlenecks & Solutions

| Problem | Solution |
|--------|---------|
| High traffic | Auto scaling |
| DB overload | Caching |
| Delivery delay | Smart routing |
| Payment failure | Retry mechanism |

---

## 📌 11. APIs (Sample)

### Place Order
```
POST /orders
```

### Get Order
```
GET /orders/{id}
```

### Track Order
```
GET /orders/{id}/track
```

---

## 🎯 Interview Tips

- Always start with requirements
- Draw high-level diagram
- Explain data flow clearly
- Talk about scaling & trade-offs

---

## 🚀 One-Line Summary

> This is an event-driven, scalable microservices architecture using caching, queues, and real-time tracking to handle high traffic efficiently.
