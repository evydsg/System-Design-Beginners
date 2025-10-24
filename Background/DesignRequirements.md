## **System Design Requirements**

### **Key Goals of System Design**

1. **Moving Data**:
    - Data is moved between servers, networks, and clients across the globe.
    - Challenges include network delays and ensuring efficient, reliable movement.
2. **Storing Data**:
    - Data must be consistent across distributed systems.
    - Storage options include:
        - **Databases**: Relational or NoSQL.
        - **Blob Stores**: Large binary objects.
        - **Distributed File Systems**: For scalability and redundancy.
3. **Transforming Data**:
    - Data is manipulated for computations, analytics, or visualization.
    - Application code or monitoring services handle transformations efficiently.

---

## **What Makes a Good Design?**

A well-designed system ensures **availability, reliability, fault tolerance, redundancy, throughput, and low latency**.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/dff36d5c-f5c3-4bab-bbb7-dd69e8da7433/cb1b6a28-be23-46c1-bdaf-9c5fe315adaf/image.png)

### **Core Metrics**

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/dff36d5c-f5c3-4bab-bbb7-dd69e8da7433/4d572b0e-1b99-4f89-bd1f-2d092457089e/image.png)

1. **Availability**:
    - Percentage of time the system is operational:
        
        Availability=Uptime + Total Time
        
    - Target: 99.999% uptime (5 minutes downtime/year).
    - Supports **Service Level Objectives (SLOs)** and **Service Level Agreements (SLAs)**.
2. **Reliability**:
    - Probability the system functions without failure.
    - Strategies:
        - Multiple servers to handle load and avoid failures.
        - Mitigation of **DDoS attacks**.
3. **Fault Tolerance**:
    - System continues operating when part of it fails.
    - Achieved through **horizontal scaling** and backup servers.
4. **Redundancy**:
    - Ensures reliability by duplicating servers or systems.
    - Types:
        - **Active-Active**: Multiple servers are active.
        - **Active-Passive**: Backup server activates only during failure.
5. **Throughput**:
    - Measures operations over time (e.g., requests/second, bytes/second).
    - Improved through:
        - **Horizontal Scaling**: Adding more servers.
        - **Vertical Scaling**: Enhancing a single server.
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/dff36d5c-f5c3-4bab-bbb7-dd69e8da7433/0bab3038-6c09-4e0c-93fa-05113aa59535/image.png)
        
        ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/dff36d5c-f5c3-4bab-bbb7-dd69e8da7433/8b72a558-e198-4e91-8957-f5f58a7f7591/image.png)
        
6. **Latency**:
- Delay between a user request and server response.
- Reduced by:
    - Using **Content Delivery Networks (CDNs)**.
    - Deploying servers closer to users geographically.
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/dff36d5c-f5c3-4bab-bbb7-dd69e8da7433/0b3bdb34-4dc8-4466-97a3-87ed8e7576e7/image.png)
    

---

## **Trade-offs in System Design**

1. **Storage**:
    - **Relational Databases**: Strong consistency but may struggle with scaling.
    - **NoSQL**: Scales better but sacrifices strict consistency.
2. **Scaling**:
    - **Vertical Scaling**: Simpler but limited by hardware.
    - **Horizontal Scaling**: Better for distributed loads but adds complexity.
3. **Data Movement**:
    - **Local Transfers**: Easier to manage but limited to smaller systems.
    - **Global Transfers**: Requires robust networks and replication strategies.

---

### **Design Thinking for System Design Interviews**

1. **Understand Requirements**:
    - Clarify data movement, storage, and transformation needs.
2. **Analyze Trade-offs**:
    - Evaluate scalability, reliability, and latency for each component.
3. **Prioritize Metrics**:
    - Focus on availability, fault tolerance, and performance metrics.