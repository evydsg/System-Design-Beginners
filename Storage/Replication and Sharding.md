# **Replication and Sharding in Distributed Systems**

Replication and sharding are two techniques commonly used together in a distributed system to achieve **high availability** and **high throughput**. 

## **1. Replication**

Replication involves creating **copies of a database** (called replicas) to distribute the workload across multiple machines, ensuring **data availability, scalability, and durability**.

### **Leader-Follower Architecture**

- The **original database** is called the **leader (or master)**.
- The **replicas** are called **followers (or slaves)**.
- The leader is responsible for **writing data**, while followers receive **replicated data** from the leader.

> Note: Data replication flows from leader to follower to ensure consistency. If data were replicated from follower to leader, the leader might not be fully updated.
> 

### **Types of Replication**

Replication can be performed in two ways:

### **1.1. Synchronous Replication**

- Every write transaction on the **leader** is **immediately** copied to the **follower**.
- Ensures **strong consistency** between replicas.
- **Downside:** Increases **latency** since transactions must wait for replication to complete.
- **Benefit:** If the **leader fails**, the follower can **take over** as the new leader with minimal data loss, ensuring **high availability**.

### **1.2. Asynchronous Replication**

- The leader does **not wait** for the follower to update before committing transactions.
- **Faster writes**, but there's a chance of data loss if the leader crashes before the follower catches up.
- Common in scenarios where **performance** is prioritized over **strict consistency**.

![image.png](attachment:3608e7fd-c725-4241-8493-88336ceea1cf:image.png)

# **Master-Master Replication and Sharding in Distributed Systems**

## **1. Master-Master (Multi-Master) Replication**

Master-Master replication is used when data needs to be served in **different regions**, enabling multiple leaders (masters) to **handle writes and reads** simultaneously.

### **Key Features**

- Each **leader serves a specific region** (e.g., one for the West, another for the East).
- Allows for **distributed writes and reads**, improving availability.
- Ensures **data is available closer to users**, reducing latency.
- Ideal for **globally distributed applications**.

### **Challenges**

- **Synchronization latency** between the masters can lead to **conflicts**.
- Requires **periodic updates** or conflict resolution mechanisms.
- More **complex to manage** compared to leader-follower (single-master) replication.

### **Asynchronous Replication**

- **Writes are not immediately synchronized** across all masters.
- **Faster writes**, but data might be **inconsistent** for a short period.
- Suitable for scenarios where **eventual consistency** is acceptable.

---

## **2. Sharding**

Sharding is used when replication alone is insufficient to handle high traffic. It involves **splitting a database** into multiple, smaller **shards**, each hosted on a separate machine or server.

### **Key Benefits**

- **Improves performance** by distributing the workload.
- **Enhances scalability**, as each shard handles only a portion of requests.
- **Increases availability**, reducing the impact of failures.

### **Data Partitioning in Sharding**

A **shard key** is used to determine how data is divided across shards.

### **2.1. Range-Based Sharding**

- Data is partitioned into **ranges**.
- Example: Splitting 100 rows across **four shards**:
    - Shard 1 → IDs **1-25**
    - Shard 2 → IDs **26-50**
    - Shard 3 → IDs **51-75**
    - Shard 4 → IDs **76-100**
- Other examples:
    - **Shard key based on gender** (Male vs. Female).
    - **Shard key based on names** (A-L vs. M-Z).

### **2.2. Hash-Based Sharding**

- Uses a **hash function** to determine the shard for each piece of data.
- Distributes data **evenly** across shards.
- **Consistent hashing** minimizes data movement when adding/removing nodes.

---

## **3. Challenges with Sharding**

While sharding enhances scalability, it presents challenges:

### **3.1. Data Distribution Complexity**

- Ensuring **related data** (from different tables) stays in the same shard is difficult.
- Queries involving **multiple shards** require **cross-shard joins**, increasing latency.

### **3.2. ACID Compliance**

- **Relational databases (SQL)**, such as MySQL and PostgreSQL, are **not designed for sharding**.
- Enforcing **ACID (Atomicity, Consistency, Isolation, Durability)** is difficult.
- Developers must implement **sharding logic manually** at the application level.

### **3.3. NoSQL and Eventual Consistency**

- **NoSQL databases** (e.g., MongoDB, Cassandra) are **designed for sharding**.
- They follow an **eventual consistency model** rather than strict ACID compliance.
- Data **does not need to be instantly consistent**, just **eventually**.

### **3.4. Consistent Hashing for Sharding**

- Used in **hash-based sharding** to evenly distribute data.
- Reduces data movement when **nodes are added/removed**.
- Helps **maintain load balance** across shards.