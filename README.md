# 🏗️ System Design for Beginners

Personal learning notes and summaries based on [NeetCode's System Design for Beginners](https://neetcode.io/courses/system-design-for-beginners) series. Covers foundational concepts across scalability, networking, storage, caching, APIs, and more — organized for easy review and interview prep.

---

## 📁 Topics Covered

| Topic | Key Concepts |
|-------|-------------|
| **Background** | Computer architecture, scaling fundamentals, vertical vs. horizontal scaling |
| **Networking** | TCP/IP, DNS, HTTP/HTTPS, latency vs. throughput |
| **APIs** | REST, GraphQL, WebSockets, API design principles |
| **Proxies** | Forward proxies, reverse proxies, load balancers |
| **Caching Basics** | Cache strategies (write-through, write-back, eviction policies), CDNs, Redis |
| **Storage** | SQL vs. NoSQL, replication, sharding, ACID vs. BASE |
| **Big Data** | Message queues, stream processing, batch vs. real-time |

---

## 🗂️ Repository Structure

```
System-Design-Beginners/
├── Background/
├── Networking/
├── APIs/
├── Proxies/
├── Caching Basics/
├── Storage/
└── Big Data/
```

---

## 🎯 How to Use This Repo

- **Sequential learning:** Follow the folders in order — start with Background and Networking before moving into APIs, Proxies, Caching, Storage, and Big Data.
- **Interview prep:** Each folder maps to a common system design interview domain. Use the notes as a quick refresher before mock interviews or on-sites.
- **Personal reference:** Notes include key concepts, real-world examples, and personal insights to make the material stick.

---

## 🔑 Core System Design Concepts at a Glance

**Scalability**
- *Vertical scaling* — add more power to one machine
- *Horizontal scaling* — add more machines; requires load balancing and stateless services

**CAP Theorem**
- A distributed system can only guarantee two of: Consistency, Availability, Partition Tolerance

**Common Tradeoffs**
- SQL vs. NoSQL — structured/relational data vs. flexible/scalable schemas
- Latency vs. throughput — fast individual responses vs. high overall data volume
- Consistency vs. availability — especially relevant during network partitions

---

## 📚 Source

All notes are derived from **[NeetCode's System Design for Beginners](https://neetcode.io/courses/system-design-for-beginners)** course. Highly recommended as a starting point for anyone preparing for software engineering interviews.

---

## 👩‍💻 Author

**Evelise** — [@evydsg](https://github.com/evydsg)
