# **NoSQL Databases Overview**

### **What is NoSQL?**

- NoSQL stands for **"Not Only SQL"** and differs fundamentally from traditional relational databases.
- Unlike SQL databases, **NoSQL databases do not use tables** or standard SQL syntax for queries and joins.
- They are **highly flexible and scalable**, designed to overcome SQL databases' scalability and performance limitations.
- **SQL databases scale vertically**, but NoSQL databases support **horizontal scaling**, which is essential for handling large applications.

---

## **Types of NoSQL Databases**

NoSQL databases are categorized into four major types:

### **1. Key-Value Databases**

- Store **key-value pairs**, similar to a **hashmap**.
- **Schemaless**: Different keys can have completely different structures.
- **Example Structure**:
    
    ```json
    {
      "user:123": { "name": "John Doe", "age": 30, "email": "johndoe@example.com" },
      "product:456": { "name": "Widget", "price": 9.99, "description": "A useful widget" }
    }
    
    ```
    
- **Example Use Case**: **Redis** (in-memory key-value store)
    - Stores data in RAM, making it extremely fast for retrieval.

---

### **2. Document Databases**

- Store data in **JSON-like documents**.
- **Flexible schema**: Fields can be added/removed independently.
- **Example Structure**:
    
    ```json
    {
      "field1": {
        "onetype": [
          { "id": 1, "name": "John Doe" },
          { "id": 2, "name": "Don Joeh" }
        ],
        "othertype": { "id": 2, "company": "ABC" }
      },
      "field2": {
        "list1": [[1, 42], [2, 2]]
      }
    }
    
    ```
    
- **Example Use Case**: **MongoDB**
    - Stores JSON-like structures for seamless integration with application code.

---

### **3. Wide-Column Databases**

- Stores data **in columns** instead of rows, optimizing for **high write throughput**.
- **Efficient for large-scale data** like internet search and web messaging systems.
- **Example Structure (Cassandra Example)**:
    
    ```
    Row Key: Location_ID (e.g., 'location1')
    Columns:
      - Timestamp1: Temperature1
      - Timestamp2: Temperature2
      - Timestamp3: Temperature3
    
    ```
    
- **Example Use Cases**: **Cassandra, Google BigTable**
    - Used in large-scale applications requiring **massive storage and retrieval**.

---

### **4. Graph Databases**

- Represent data using **nodes (entities)** and **edges (relationships)**.
- Useful for modeling **complex relationships** (e.g., social networks).
- **Example Use Case**: **Facebook**
    - Tracks **friend connections, likes, comments, and shares** efficiently.
- **Example Databases**: **Neo4j, Amazon Neptune**


---

## **Why Use NoSQL Databases?**

### **Key Benefits**

1. **Scalability**
    - **Horizontally scalable** across multiple servers.
    - Unlike SQL databases, which require expensive vertical scaling, NoSQL databases can be **distributed across different regions**.
2. **Flexible Schema**
    - No need for predefined schemas, making NoSQL ideal for **rapidly evolving applications**.
3. **High Availability**
    - **Distributed architecture** eliminates a **single point of failure**.
4. **Optimized for Big Data**
    - Handles **large-scale data and high-speed workloads** efficiently.

---

## **Consistency Models: ACID vs BASE**

### **ACID (SQL Databases)**

- **A**tomicity (all-or-nothing transactions)
- **C**onsistency (ensures valid state)
- **I**solation (transactions are independent)
- **D**urability (data is permanently stored)

### **BASE (NoSQL Databases)**

- **B**asically Available (system guarantees availability)
- **S**oft State (state may change over time)
- **E**ventual Consistency (data updates eventually propagate across all nodes)

### **Eventual Consistency in NoSQL**

- **Leader-Follower Architecture**
    - **Writes happen on the primary node** (leader).
    - The leader **replicates data to follower nodes**.
    - Users **may see stale data** temporarily, but it updates **eventually**.
    - Example: **Twitter and Instagram**
        - Follower count updates may be delayed due to replication lag.
        

### **Conclusion**

- NoSQL databases are designed for **modern, large-scale applications** where scalability, flexibility, and performance matter.
- Each NoSQL type is specialized for different use cases:
    - **Key-Value Stores** → Caching, session storage (e.g., Redis)
    - **Document Stores** → Content management, e-commerce (e.g., MongoDB)
    - **Wide-Column Stores** → Analytical workloads, time-series data (e.g., Cassandra)
    - **Graph Databases** → Social networks, recommendation engines (e.g., Neo4j)