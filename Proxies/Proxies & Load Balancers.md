# Proxies & Load Balancers

## 1. Proxies

Proxies act as intermediaries between clients and servers to manage network traffic, improve security, and optimize performance.

### 1.1 Forward Proxy

A forward proxy server functions as an intermediary between clients and the internet, masking the client's identity and controlling access to network resources.
### **How It Works:**

- Clients send requests to the proxy server.
- The proxy server forwards the requests to the destination (e.g., a website).
- The origin server sees the proxy's IP address instead of the client's IP.
- The proxy can cache responses, restrict access, or filter requests based on configured policies.

### **Benefits:**

- Provides privacy by hiding the client’s IP address.
- Increases efficiency through caching.
- Controls network traffic by filtering requests.

### **Example Use Cases:**

- Anonymous browsing
- Enforcing network security policies
- Caching frequently accessed content

### 1.2 Reverse Proxy

A reverse proxy sits in front of web servers, handling incoming client requests and distributing them to the appropriate backend servers.
### **How It Works:**

- Clients send requests to the reverse proxy instead of directly accessing the origin server.
- The reverse proxy forwards the request to the appropriate backend server.
- The client does not know which backend server processed the request.

### **Benefits:**

- Enhances security by masking the server's identity.
- Balances load across multiple servers.
- Protects against DDoS attacks.
- Improves performance through caching.

### **Example Use Cases:**

- **Content Delivery Networks (CDNs)**: Serve cached static content to reduce server load.
- **Application Firewalls**: Protect backend servers from malicious traffic.
- **API Gateways**: Manage and secure API traffic.

## 2. Load Balancers

Load balancers distribute incoming network traffic across multiple servers to ensure efficient resource utilization and prevent server overload.

### 2.1 Load Balancing Strategies

### **1. Round Robin**
- Requests are distributed sequentially across all available servers in a circular order.
- Ensures even distribution of traffic.
- Works best when all servers have similar processing capabilities.

### **2. Weighted Round Robin**
- Requests are distributed based on each server’s assigned weight.
- Servers with higher processing power receive more requests.
- Ideal for environments with heterogeneous server capacities.

## 3. Least Connections
- Requests are directed to the server with the fewest active connections.
- Helps balance uneven request loads.
- Useful in scenarios where requests have variable processing times.

### **4. Location-Based Routing**

- Requests are directed to the geographically closest server to minimize latency.
- Enhances performance for globally distributed users.
- Commonly used in CDNs.

### **5. Hashing**

- Uses a hashing algorithm to assign requests to servers based on IP addresses or session IDs.
- Ensures consistency in request routing (e.g., always directing a particular user to the same server).

### 2.2 Load Balancing at Different Network Layers

### **Layer 4 (Transport Layer - TCP/UDP)**

- Routes traffic based on IP addresses and TCP ports.
- Does not inspect the content of the request.
- Faster and more efficient but lacks application-specific routing capabilities.

### **Layer 7 (Application Layer - HTTP/HTTPS)**
- Routes traffic based on application-level data (e.g., URL paths, headers, cookies).
- Enables advanced routing and content-based load balancing.
- Allows routing requests based on user-specific attributes.

## 3. Summary
| Feature | Forward Proxy | Reverse Proxy | Load Balancer |
| --- | --- | --- | --- |
| **Hides** | Client | Server | Neither (optimizes distribution) |
| **Traffic Direction** | Outbound (Client → Internet) | Inbound (Client → Server) | Bidirectional (Client ↔ Server) |
| **Security** | Protects clients from exposure | Protects backend servers | Ensures even request distribution |
| **Performance Enhancement** | Caching, Filtering | Load distribution, Caching | Load balancing |
| **Use Cases** | Anonymous browsing, Content filtering | CDNs, API Gateways, Security | Web applications, Databases, Cloud services |