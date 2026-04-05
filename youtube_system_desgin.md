# 🎬 Video Streaming System — File System Design (Storage Deep Dive)

---

## 📌 1. Goal

Design a **scalable file storage system** for a video platform (like YouTube/Netflix) that:
- Stores large video files
- Supports fast upload/download
- Ensures durability and availability

---

## 📌 2. Requirements

### ✅ Functional
- Upload large video files
- Store video in chunks
- Retrieve video efficiently
- Support multiple resolutions (480p, 720p, 1080p)

### ⚡ Non-Functional
- High durability (no data loss)
- High availability
- Efficient storage
- Fast read performance

---

## 📌 3. Storage Architecture

```
Client
  ↓
Upload Service
  ↓
Chunking Service
  ↓
-------------------------
| Object Storage (S3)   |
| Distributed File Nodes|
-------------------------
  ↓
Metadata Service → DB
```

---

## 📌 4. Key Concepts

### 📦 1. Chunking (Very Important ⭐)

- Large video split into smaller chunks (e.g., 5MB each)

```
video.mp4 → chunk1, chunk2, chunk3...
```

#### Why?
- Faster upload
- Retry failed chunks
- Parallel processing

---

### 🧠 2. Metadata Management

Store metadata in DB:

```
video_id
user_id
chunk_ids[]
resolution_versions[]
upload_time
```

---

### 💾 3. Object Storage (S3-like)

- Stores actual video chunks
- Each chunk stored as:
```
/videos/{video_id}/chunk_1
/videos/{video_id}/chunk_2
```

---

### 🎥 4. Video Versions

Each video has multiple formats:

```
video_480p
video_720p
video_1080p
```

---

## 📌 5. Upload Flow (File System Perspective)

1. User uploads video
2. File split into chunks
3. Each chunk uploaded independently
4. Stored in Object Storage
5. Metadata stored in DB
6. Trigger video processing (transcoding)

---

## 📌 6. Download / Streaming Flow

1. User requests video
2. Metadata fetched
3. CDN serves chunks
4. Player streams chunks sequentially

---

## 📌 7. Replication (Durability 🔥)

- Each chunk stored in multiple nodes:

```
Chunk1 → Node A, Node B, Node C
```

### Benefits:
- Fault tolerance
- No data loss

---

## 📌 8. Storage Optimization

### 🔹 Compression
- Reduce file size

### 🔹 Deduplication
- Avoid storing duplicate content

### 🔹 Lifecycle Management
- Move old videos to cold storage

---

## 📌 9. Scaling Strategy

### 🔥 Horizontal Scaling
- Add more storage nodes

### 🔥 Partitioning
- Partition by video_id

### 🔥 CDN
- Cache frequently accessed videos

---

## 📌 10. Failure Handling

| Problem | Solution |
|--------|---------|
| Chunk upload failure | Retry only failed chunk |
| Node failure | Use replicated copy |
| Corrupted file | Checksum validation |

---

## 📌 11. Data Integrity

- Use checksum (MD5/SHA)
- Validate chunks before merging

---

## 📌 12. Advanced Concepts (Interview Booster 🚀)

- Erasure Coding (better than replication)
- Multi-region replication
- Pre-signed URLs for upload
- Rate limiting uploads

---

## 🎯 Interview Tips

Say these lines:

👉 “I will use chunking for large file upload”  
👉 “Object storage like S3 will store chunks”  
👉 “Replication ensures durability”  
👉 “CDN improves read performance”  

---

## 🚀 One-Line Summary

> A distributed file storage system using chunking, object storage, replication, and CDN to efficiently store and stream large video files.
