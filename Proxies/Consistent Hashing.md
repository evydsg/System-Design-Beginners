# **Consistent Hashing**

## **Introduction**

Hashing is a technique used to map requests to servers in the context of load balancing. Similar to hash functions in data structures and algorithms, consistent hashing ensures that each request, identified by an IP address, user ID, or request ID, is consistently assigned to the same server.

---

## **How Regular Hashing Works**

- Each request has a unique identifier (e.g., IP address).
- The server is assigned using the formula:
    
    Hash(IP Address) % Number of Servers= Assigned Server
    
- **Example:**
    - Suppose we have three servers (0, 1, and 2).
    - Incoming requests with IP addresses 6, 7, and 8 are assigned as follows:
        
        ```
        6 % 3 = 0  →  Server 0
        7 % 3 = 1  →  Server 1
        8 % 3 = 2  →  Server 2
        
        ```
        
- The same IP address always gets assigned to the same server, allowing each server to cache user-specific data efficiently.
- This differs from **Round Robin**, where assignments are sequential and not consistent.


---

## **Issues with Regular Hashing**


A major drawback arises when a server fails:

- If **Server 2 goes down**, we need to recompute assignments.
- With only **Servers 0 and 1** remaining, the mapping changes:
    
    ```
    9 % 2 = 1  →  Server 1
    10 % 2 = 0  →  Server 0
    11 % 2 = 1  →  Server 1
    
    ```
    
- This re-mapping causes **cache misses**, as previous user data might be lost or stored on a different server.

---

## **Consistent Hashing: The Solution**

Consistent hashing ensures **better load distribution** while **minimizing disruptions** when a server goes down. It achieves this through:

- A **ring-based structure** that represents all possible hash values.
- A **hash function** that maps both **servers** and **requests** to points on this ring.
- **Clockwise assignment**, meaning:
    - If a server fails, its requests are reassigned to the next available server in the ring.

---

## **How Consistent Hashing Works**

1. **Hash the IP Address and place it on the ring.**
2. **Hash each server and place it on the ring.**
3. **Find the closest server in a clockwise direction** from the request’s position.
4. If a server fails, only requests mapped to that server need to be reassigned, rather than all requests.

### **Example:**

- **Before failure:**
    - Request 6 → Server 0
    - Request 7 → Server 1
    - Request 8 → Server 2
- **If Server 2 fails:**
    - Requests originally assigned to **Server 2** now go to the **next available server (Server 0).**
- This **reduces cache misses** and **maintains load balance** efficiently.

---

## **Mathematical Implementation**

- Hash values are calculated using:
    
    Hash(IP Address)mod  M\text{Hash(IP Address)} \mod M
    
    where **M** is the number of positions on the ring.
    
- The **modulus operation** ensures:
    - Requests are uniformly distributed.
    - Overflow issues are prevented.

---

### **Key Benefits of Consistent Hashing**

✅ **Minimizes reassignments** when a server fails.

✅ **Ensures consistent mapping** of requests.

✅ **Efficient load balancing** across available servers.

✅ **Reduces cache misses**, improving system performance.