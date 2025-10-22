# Application Architecture
## **How Developers View the System**

Developers write code, which is then deployed to a **server**. A server is essentially a computer designed to handle requests from other devices. This server often needs **persistent storage** to save data, such as user information or application settings.

- **Storage:** While some servers have built-in storage, it’s often limited in size. Instead, servers commonly use external storage systems like databases or cloud storage, which are connected through a network.

---

## **How Users View the System**

From a user’s perspective, interaction happens through a **client**, such as a web browser or a mobile app. When users request something (e.g., loading a webpage or submitting a form), the server processes the request and sends back the necessary resources, like HTML, CSS, or JavaScript.

But what happens if the server gets overwhelmed by too many requests? This is where **scaling** becomes important.

---

## **Scaling Servers**

### **Vertical Scaling**

- **What it is:** Upgrading the resources of a single server, like adding more RAM or switching to a faster CPU.
- **Limitations:** Each server has a maximum capacity, so there’s a limit to how much you can upgrade.

### **Horizontal Scaling**

- **What it is:** Adding more servers to handle the load. Instead of one powerful server, multiple servers share the work.
- **Benefits:**
    - Distributes the workload, ensuring no single server is overwhelmed.
    - Provides redundancy—if one server fails, others can take over.
- **Challenges:** Requires additional effort to coordinate the servers and distribute requests evenly.

---

## **Load Balancer**

In systems with multiple servers, a **load balancer** ensures that user requests are distributed fairly across all servers. This prevents any single server from becoming overloaded and helps maintain performance.

---

## **Logging and Metrics**

### **Logging**

- Logs are like a diary for servers, recording all activities and errors.
- **Purpose:** Helps developers track what happened, identify bugs, and diagnose issues when a server crashes.

### **Metrics**

- Metrics collect performance data, such as CPU usage, memory consumption, and network traffic.
- **Purpose:** Helps developers understand how the system is performing and identify bottlenecks.
- Metrics provide a bigger picture than logs by highlighting overall trends and resource usage.

---

## **Alerts**

Manually monitoring metrics all the time isn’t practical. Instead, developers set up **alerts** to notify them when something goes wrong.

For example:

- If server response success rates drop below 95%, developers can receive an alert.
- Alerts act like push notifications, letting developers respond quickly to issues without constantly checking metrics.

---

By combining these components—**scaling, load balancing, logging, metrics, and alerts**—modern applications can handle large user bases efficiently while maintaining reliability and performance.