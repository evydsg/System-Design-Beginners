# 📦 Design: Google Drive (Cloud Storage System)

## 🔗 Source
Original notes: :contentReference[oaicite:0]{index=0}

---

## 🧠 Problem Overview
Design a scalable cloud storage system similar to Google Drive that allows users to:
- Store files (documents, images, videos)
- Organize files into folders
- Share files with others
- Access files reliably from anywhere

---

## ⚙️ Core Operations

### 📌 User Actions
- Upload files
- Download files
- Delete files
- Edit files (docs, spreadsheets, PDFs)
- Share files
- Create/manage folders

---

## ✅ Functional Requirements

- Upload files
- Download files
- Delete files
- Organize files in folders
- Share files with permissions
- Edit supported file types

---

## 🚀 Non-Functional Requirements

### 📊 Scale
- ~200M total users
- ~50M daily active users (DAU)
- Free tier: 15GB per user
- Paid users: higher storage limits

### 📈 Performance
- Read-heavy system (read:write ≈ 2:1)
- Average file size: ~10MB
- Latency is less critical than availability

### 🔒 Reliability & Availability
- High availability (critical for user trust)
- Strong durability (no data loss)
- Data replication across multiple regions

---

## 💾 Storage Estimation

- 200M users × 15GB = **~3 Exabytes total storage**
- Requires:
  - Distributed storage
  - Replication (e.g., 3x copies)
  - Efficient space usage (deduplication)

---

## 🏗️ High-Level Architecture

```

Client → App Server → Object Storage
→ Metadata Store (Key-Value DB)
→ Cache Layer

```

### 🔹 Components

#### 1. Client
- Web / Mobile apps
- Handles uploads, downloads, UI

#### 2. App Server
- Authentication
- File operations logic
- Access control & permissions

#### 3. Object Storage (Blob Storage)
- Stores actual file data (images, videos, etc.)
- Examples: AWS S3, Azure Blob Storage
- Highly scalable and durable

#### 4. Metadata Store
- Stores:
  - File names
  - Ownership
  - Permissions
  - File location (pointer to object storage)
- Implemented using:
  - NoSQL (key-value store)
  - SQL (optional for relational queries)

#### 5. Cache
- Speeds up frequently accessed metadata/files
- Not critical but improves performance

---

## 📂 File Storage Design

### 🔹 Block-Level Storage
- Files are split into **chunks (blocks)**
- Each block stored in object storage
- Reassembled when user downloads

### 🔹 Benefits
- Parallel uploads/downloads
- Efficient retries (only failed chunks re-uploaded)
- Better scalability

---

## ♻️ Deduplication

- Avoid storing duplicate files globally
- Use **content-based hashing**
- Store only one copy of identical content

### 📌 Example
- If 1M users upload the same file:
  → Store only ONE copy

---

## 🧩 Content Addressable Storage (CAS)

- Files identified by hash of their content
- Enables:
  - Deduplication
  - Integrity checks
  - Efficient storage

---

## 🗂️ Folder Structure

- Folders are **logical abstractions**
- Implemented via metadata (not physical structure)

### 📌 Key Idea
- Files store references (pointers)
- Folder = collection of references

---

## 🗑️ Deletion Strategy

- File is NOT immediately deleted
- Instead:
  - Remove reference for that user
  - Keep file if other users still reference it

### 🧹 Garbage Collection
- Periodically:
  - Scan metadata
  - Remove unreferenced data (blobs)

---

## 🔁 Data Replication

- Replicate data across:
  - Multiple servers
  - Multiple data centers

### 🎯 Goal
- Ensure durability and fault tolerance

---

## 📡 Reliability Mechanisms

### ❤️ Heartbeats
- Servers send periodic signals to indicate they are alive

### 🧠 Coordination Systems
- Tools like:
  - Zookeeper
  - Kafka

Used for:
- Service coordination
- Failure detection

---

## ⚖️ Load Balancing

- Distribute traffic across servers
- Prevent overload
- Improve availability

---

## 🔐 Access Control

- Managed at App Server layer
- Controls:
  - File visibility (private/public/shared)
  - Permissions (read/write)

---

## 📁 Object Storage vs File System

| Feature            | File System (HDFS) | Object Storage |
|-------------------|------------------|---------------|
| Structure         | Hierarchical     | Flat          |
| Scalability       | Limited          | Highly scalable |
| Mutability        | Mutable          | Mostly immutable |
| Examples          | HDFS             | S3, Azure Blob |

---

## 🔄 Upload Flow

1. Client splits file into chunks
2. Uploads chunks in parallel
3. Chunks stored in object storage
4. Metadata saved in DB
5. File reconstructed logically

---

## 🔄 Download Flow

1. Client requests file
2. Metadata retrieved
3. Chunks fetched from object storage
4. File reassembled and returned

---

## ⚠️ Failure Handling

- If upload fails mid-way:
  → Resume from last successful chunk
- Retry mechanism for failed chunks

---

## 📌 Key Design Decisions

- Use **Object Storage** for scalability
- Use **Key-Value store** for metadata
- Implement **deduplication** to save space
- Prioritize **availability over latency**
- Use **replication + heartbeats** for reliability

---

## 💡 Interview Tips

- Always mention:
  - Scalability (millions of users)
  - Trade-offs (latency vs availability)
  - Storage optimization (deduplication)
  - Fault tolerance (replication, retries)
- Draw architecture diagram if possible
- Clarify assumptions early

---

## 🧠 Summary

A Google Drive-like system is:
- **Distributed**
- **Highly available**
- **Storage-efficient**
- **Fault-tolerant**

Built using:
- Object storage + metadata DB
- Chunking + deduplication
- Replication + monitoring

Perfect — let’s upgrade this to **“final boss system design notes”** with clean, interview-ready diagrams you can literally draw on a whiteboard or explain out loud.

---

## 🧠 1. High-Level Architecture


    ┌───────────────┐
    │    Client     │
    │ (Web/Mobile)  │
    └──────┬────────┘
           │
           ▼
    ┌───────────────┐
    │  API Gateway  │
    └──────┬────────┘
           │
```

┌───────────┼────────────┐
▼           ▼            ▼
┌────────┐  ┌──────────┐  ┌──────────┐
│ Auth   │  │ File Svc │  │ Share Svc│
└────────┘  └────┬─────┘  └──────────┘
│
┌────────┼────────┐
▼        ▼        ▼
┌──────────┐ ┌──────────┐ ┌──────────┐
│ Metadata │ │  Cache   │ │  Queue   │
│   DB     │ │ (Redis)  │ │ (Kafka)  │
└────┬─────┘ └──────────┘ └──────────┘
│
▼
┌───────────────┐
│ Object Storage│
│   (S3/Blob)   │
└───────────────┘

```

### 🔥 Key Idea
- **Metadata ≠ File data**
- Metadata → DB  
- Files → Object Storage

---

## 📂 2. Upload Flow (Chunk-Based)

```

Client
│
│ Split file into chunks
▼
Upload Service
│
├── Upload Chunk 1 ──► Object Storage
├── Upload Chunk 2 ──► Object Storage
├── Upload Chunk 3 ──► Object Storage
│
▼
Metadata DB (store chunk references)

```

### ✅ Benefits
- Parallel uploads
- Resume on failure
- Efficient large file handling

---

## 📥 3. Download Flow

```

Client Request
│
▼
File Service
│
▼
Metadata DB ──► Get chunk locations
│
▼
Object Storage ──► Fetch chunks
│
▼
Reassemble file
│
▼
Return to client

```

---

## 🧩 4. Deduplication (Content Addressable Storage)

```

File Upload
│
▼
Generate Hash (SHA-256)
│
▼
Check if hash exists?
│
┌─┴───────────────┐
│ YES             │ NO
▼                 ▼
Reuse existing     Store new file
file reference     in storage

```

### 💡 Result
- 1 file stored globally  
- Millions of users can reference it

---

## 🗂️ 5. Folder Structure (Logical, Not Physical)

```

User Root
│
├── Folder A
│     ├── File1 (pointer → storage)
│     └── File2 (pointer → storage)
│
└── Folder B
└── File1 (same pointer reused)

```

### 🔥 Insight
- Folders = **metadata only**
- Files are NOT duplicated

---

## 🗑️ 6. Deletion + Garbage Collection

```

User deletes file
│
▼
Remove reference (metadata)
│
▼
Still referenced by others?
│
┌────┴──────────┐
│ YES           │ NO
▼               ▼
Keep file     Mark for deletion
│
▼
Garbage Collector
│
▼
Delete from storage

```

---

## 🔁 7. Replication & Reliability

```

```
    ┌──────────────┐
    │   Region A   │
    └──────┬───────┘
           │
  ┌────────┼────────┐
  ▼        ▼        ▼
```

Copy 1   Copy 2   Copy 3

(Stored across multiple data centers)

```

### ✅ Guarantees
- High durability (99.999999999%)
- Fault tolerance

---

## ❤️ 8. Heartbeat & Monitoring

```

Storage Node ────► "I'm alive" ────► Coordinator (Zookeeper)
Storage Node ────► "I'm alive" ────► Monitoring System

If heartbeat stops:
→ Node is considered DOWN
→ Traffic redirected

```

---

## ⚖️ 9. Load Balancing

```

```
       ┌─────────────┐
       │ Load Balancer│
       └──────┬──────┘
              │
  ┌───────────┼───────────┐
  ▼           ▼           ▼
```

Server 1    Server 2    Server 3

```

### 🎯 Goal
- Even traffic distribution
- Prevent overload

---

## 🔐 10. Access Control Flow

```

User → Request file
│
▼
Auth Service → Validate identity
│
▼
Permission Check
│
┌──────┴────────┐
│ Allowed       │ Denied
▼               ▼
Serve file     Reject request

```

---

## 🧠 11. Data Model

### Metadata (DB)
```

File {
file_id
owner_id
file_name
size
chunk_ids[]
permissions
}

```

### Chunk Mapping
```

Chunk {
chunk_id
storage_location
hash
}

```

---

## ⚡ 12. Key Design Insights (Interview Gold)

- Separate **metadata vs file storage**
- Use **chunking for scalability**
- Use **deduplication for cost savings**
- Use **replication for reliability**
- Use **eventual consistency for scale**
- Folders are **just pointers**

---

## 🧠 Final Summary

```

Google Drive =

Object Storage

* Metadata DB
* Chunking
* Deduplication
* Replication
* Strong availability

```
