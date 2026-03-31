# 🏗️ URL Shortener — System Design (Interview Notes)

---

## 🎯 Problem Statement

Design a system like a URL shortener that:

* Converts long URLs into short URLs
* Redirects users from short URL → original URL

---

## 🧠 High-Level Idea

### Input:

```
https://www.example.com/very/long/url
```

### Output:

```
https://short.ly/abc123
```

---

## 🧩 Core Components

### 1. API Service

* Accepts long URL
* Returns short URL

### 2. Database

* Stores mapping:

```
short_id → long_url
```

### 3. Redirect Service

* Takes short URL
* Looks up original URL
* Redirects user

---

## 🔑 How to Generate Short ID

### ✅ Option 1: Auto Increment + Base62 (Recommended)

* Example:

  * ID: `1001`
  * Base62: `g7`

**Why Base62?**

* Uses: `a-z`, `A-Z`, `0-9`
* Total = 62 characters → shorter URLs

---

### ⚠️ Option 2: Hashing (MD5/SHA)

* Hash long URL → take first few chars

**Problem:**

* Collisions possible

---

### ⚠️ Option 3: Random String

* Generate random 6-character string

**Problem:**

* Must check for collisions

---

### ⭐ Best Answer (Interview)

* Auto increment + Base62
* OR distributed ID generator (e.g., Snowflake)

---

## 🗄️ Database Design

### Basic Schema:

```
short_id | long_url
```

### Extended Schema:

```
short_id | long_url | created_at | expiry
```

---

## 🧱 Database Choice

### SQL (MySQL/Postgres)

* Easy to start
* Strong consistency

### NoSQL (MongoDB/DynamoDB)

* Better scalability

**Interview Tip:**

> Start with SQL → move to NoSQL when scaling

---

## 🔄 Redirect Flow

1. User clicks:

```
short.ly/abc123
```

2. Server extracts:

```
abc123
```

3. Lookup in DB:

```
→ original URL
```

4. Return:

```
HTTP 301 / 302 Redirect
```

---

## ⚡ Scaling Considerations

### 1. Caching (Very Important)

* Use Redis

Flow:

```
Cache → DB → Cache update
```

---

### 2. Read Heavy System

* Reads >> Writes

**Optimizations:**

* Cache layer
* Read replicas

---

### 3. Load Balancer

* Distributes traffic across servers

---

### 4. CDN (Optional)

* Faster global redirection

---

## 🚨 Edge Cases

### Duplicate URLs

* Same long URL → same short URL? (optional)

---

### Expiry

* Links may expire after certain time

---

### Custom Alias

```
short.ly/deepa
```

---

### Analytics (Bonus)

Track:

* Click count
* Location
* Device

---

## 🧩 End-to-End Flow

### URL Creation:

```
User → API → Generate ID → Store in DB → Return short URL
```

### Redirection:

```
User → Short URL → Cache → DB → Redirect
```

---

## 🎯 Final Interview Answer (Must Remember)

A URL shortener works by generating a unique short ID (typically using Base62 encoding of an auto-increment ID), storing a mapping of short ID to long URL in a database, and redirecting users by looking up the short ID and returning the original URL using HTTP redirects. To scale, caching (Redis), load balancing, and database replication are used since the system is read-heavy.

---

## 🏗️ High-Level Design (HLD)

### 📊 Architecture Overview

```
            ┌───────────────┐
            │     Client    │
            └──────┬────────┘
                   │
                   ▼
            ┌───────────────┐
            │  Load Balancer│
            └──────┬────────┘
                   │
        ┌──────────┴──────────┐
        ▼                     ▼
┌───────────────┐     ┌───────────────┐
│  API Servers  │     │ Redirect Svc  │
└──────┬────────┘     └──────┬────────┘
       │                     │
       ▼                     ▼
┌───────────────┐     ┌───────────────┐
│     Cache     │     │     Cache     │
│    (Redis)    │     │    (Redis)    │
└──────┬────────┘     └──────┬────────┘
       │                     │
       ▼                     ▼
┌─────────────────────────────────────┐
│           Database (DB)             │
└─────────────────────────────────────┘
```

### 🧠 HLD Flow

#### 🔹 URL Creation

```
Client → LB → API → Generate ID → DB → Return Short URL
```

#### 🔹 Redirection

```
Client → LB → Redirect Service → Cache → DB → Redirect
```

---

## 🔬 Low-Level Design (LLD)

### 🧱 API Design

#### 1. Create Short URL

```
POST /shorten
Body: { long_url }
Response: { short_url }
```

#### 2. Redirect

```
GET /{short_id}
→ Returns 301/302 redirect
```

---

### 🗄️ Data Model

#### Table: URL Mapping

```
id (PK)
short_id (unique)
long_url
created_at
expiry
user_id (optional)
```

---

### 🔑 ID Generation Logic

```
1. Generate unique ID (auto increment / distributed)
2. Convert to Base62
3. Check uniqueness (rare case)
```

---

### ⚡ Cache Strategy

* Key: short_id
* Value: long_url

#### Flow:

```
if (cache hit)
   return URL
else
   fetch from DB → update cache
```

---

### 🔁 Redirect Logic (Detailed)

```
1. Extract short_id from URL
2. Check Redis cache
3. If miss → query DB
4. If found → return 301 redirect
5. If not found → return 404
```

---

### 🧩 Optional Features (LLD Enhancements)

#### 🔹 Custom Alias

* Validate uniqueness
* Store directly

#### 🔹 Expiration

* Background job to delete expired links

#### 🔹 Analytics Service

* Store click events asynchronously

---

## 🚀 Follow-Up Questions (Practice)

* How would you handle 10M requests per second?
* How do you prevent abuse/spam URLs?
* How wo
