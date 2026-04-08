# 🚖 Ride Sharing System Design (Uber/Ola)

---

# 📌 1. Introduction

This document describes the system design for a scalable ride-sharing platform similar to Uber/Ola. It covers architecture, services, database design, scalability, and real-time processing.

---

# 📌 2. Requirements

## ✅ Functional Requirements
- User can book a ride
- Driver can accept/reject ride
- Real-time location tracking
- Fare estimation
- Payments (Cash, UPI, Card)
- Notifications (Push/SMS)

## ⚙️ Non-Functional Requirements
- High availability (99.99%)
- Low latency (<100ms for matching)
- Scalability (millions of users)
- Fault tolerance
- Real-time updates

---

# 🏗️ High-Level Architecture 

## 📌 Overview 

The Ride Sharing system follows a **distributed microservices architecture** designed for: - High scalability - Low latency - Real-time communication - Fault tolerance Each component is independently deployable and communicates via **REST APIs** and **event-driven messaging (Kafka)**. ---

---

# 🔁 4. Ride Flow

## 📤 Ride Request
1. User enters pickup & drop
2. API Gateway authenticates request
3. Ride Service creates ride (REQUESTED)
4. Matching Service finds drivers
5. Driver notified

## 🚗 Ride Acceptance
1. Driver accepts ride
2. Status → ACCEPTED
3. Rider notified

## 🛣️ Ride Start
1. Driver starts ride
2. Status → ONGOING
3. Location tracking begins

## ✅ Ride Completion
1. Driver ends ride
2. Status → COMPLETED
3. Payment triggered

---

# 🧩 5. Core Services

## 5.1 API Gateway
- Authentication (JWT)
- Rate limiting
- Request routing

## 5.2 Ride Service
- Create ride
- Manage lifecycle

## 5.3 Matching Service
- Finds nearest drivers
- Uses GeoHash / KD-tree

## 5.4 Location Service
- Real-time tracking
- Redis Geo indexing
- TTL for inactive drivers

## 5.5 Payment Service
- Fare calculation
- Payment processing

## 5.6 Notification Service
- Push (FCM/APNs)
- SMS fallback

## 5.7 Message Queue (Kafka)
- Async processing
- Event-driven system

---

# 🗄️ 6. Database Design

---

## 6.1 Users Table

| Column | Type | Description |
|--------|------|------------|
| id | UUID | Primary key |
| name | VARCHAR | User name |
| email | VARCHAR | Email |
| phone | VARCHAR | Phone number |
| created_at | TIMESTAMP | Created time |

---

## 6.2 Drivers Table

| Column | Type | Description |
|--------|------|------------|
| id | UUID | Primary key |
| name | VARCHAR | Driver name |
| vehicle_number | VARCHAR | Vehicle |
| status | VARCHAR | ONLINE/OFFLINE |
| rating | FLOAT | Driver rating |

---

## 6.3 Rides Table

| Column | Type | Description |
|--------|------|------------|
| id | UUID | Ride ID |
| rider_id | UUID | User |
| driver_id | UUID | Driver |
| status | VARCHAR | Ride status |
| pickup_lat | DECIMAL | Pickup lat |
| pickup_lng | DECIMAL | Pickup lng |
| drop_lat | DECIMAL | Drop lat |
| drop_lng | DECIMAL | Drop lng |
| fare_estimate | DECIMAL | Estimated fare |
| final_fare | DECIMAL | Final fare |
| requested_at | TIMESTAMP | Requested time |
| completed_at | TIMESTAMP | Completion time |

---

## 6.4 Payments Table

| Column | Type | Description |
|--------|------|------------|
| id | UUID | Payment ID |
| ride_id | UUID | Ride reference |
| amount | DECIMAL | Paid amount |
| status | VARCHAR | SUCCESS/FAILED |
| method | VARCHAR | UPI/CARD/CASH |

---

# 📊 7. Scaling Strategy

## 🚀 Horizontal Scaling
- Stateless services
- Load balancers

## 📦 Caching
- Redis for:
  - Active rides
  - Driver locations

## 📡 CDN
- Static assets delivery

## 🔁 Read Replicas
- Analytics queries

---

# 📍 8. Real-Time Location Handling

- Driver sends location every 2–5 sec
- Stored in Redis (GeoSpatial index)
- Nearby drivers fetched using radius search

---

# ⚡ 9. Matching Algorithm

- Input: Rider location
- Steps:
  1. Query nearby drivers
  2. Filter available drivers
  3. Rank by distance + rating
  4. Send request

---

# 🔔 10. Notification Flow

- Kafka event → Notification Service
- Push via FCM/APNs
- SMS fallback if failed

---

# 💳 11. Payment Flow

1. Ride completed
2. Fare calculated
3. Payment initiated
4. Status updated

---

# ⚠️ 12. Failure Handling

- Driver not responding → retry next driver
- Payment failure → retry + fallback
- Service failure → circuit breaker

---

# 🔐 13. Security

- JWT Authentication
- HTTPS everywhere
- Rate limiting
- Data encryption

---

# 📈 14. Monitoring

- Metrics: latency, errors
- Tools: Prometheus, Grafana
- Logging: ELK stack

---

# 🧠 15. Interview Tips

- Start with requirements
- Draw architecture
- Explain trade-offs
- Discuss scaling & bottlenecks

---

# 🎯 Conclusion

This design ensures:
- Scalability
- Low latency
- Fault tolerance
- Real-time experience

---
