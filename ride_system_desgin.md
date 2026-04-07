
---

# 🧩 7. Core Services Deep Dive

## 7.1 API Gateway
- Authentication (JWT)
- Rate limiting
- Routing

---

## 7.2 Ride Service
- Create ride
- Maintain lifecycle:
  REQUESTED → ACCEPTED → ONGOING → COMPLETED

---

## 7.3 Matching Service
- Finds nearest drivers
- Uses:
  - GeoHash
  - KD-tree (optional)

---

## 7.4 Location Service
- Stores real-time driver location
- Uses Redis GeoSpatial indexing
- Removes stale drivers (TTL)

---

## 7.5 Notification Service
- Push notifications (FCM/APNs)
- SMS fallback

---

## 7.6 Message Queue (Kafka)
- Decouples services
- Handles retries
- Event-driven architecture

---

# 🗄️ 8. Database Design

## 8.1 Rides Table
