# **Message Queues**

## **Introduction**

Message queues provide a solution for handling a high volume of requests when an application server cannot process them all simultaneously.  
Instead of immediately processing each request, message queues allow requests to be queued and handled later, improving efficiency and system reliability.

### **Why Not Just Scale the Server?**

While scaling horizontally (adding more servers) or vertically (increasing server capacity) is an option, it is not always cost-effective or practical.  
Additionally, some requests do not require immediate processing, making message queues a better alternative.

---

## **How Message Queues Work**

Message queues act as a **buffer** between **producers (app events)** and **consumers (application servers)**, helping manage surges in data and ensuring efficient processing.

---

## **Example: Payment Processing**

Message queues are particularly useful in **payment processing systems**.

### **Handling Peaks in Load**

- During high-traffic events like sales, the number of payment requests spikes.
- Processing payments synchronously could lead to **long wait times and potential timeouts**.
- With message queues, payments are stored and processed **asynchronously**, ensuring a smoother user experience.

### **Decoupling Services**

- When a customer places an order, a message is published to the queue.
- The **payment service** (acting as a subscriber) retrieves the message, processes the payment, and updates the order status.

---

## **Push vs. Pull Model**

Message queues can interact with application servers in two ways:

### **Pull-Based Model**

- The application continuously monitors the queue for new messages.
- If the server has capacity, it **pulls** messages from the queue and processes them.
- **Advantages:** Efficient load management, preventing server overload.
- **Disadvantages:** If the queue is empty, it may introduce latency.


### **Push-Based Model**

- The queue actively **pushes** messages to the server as soon as they arrive.
- **Advantages:** Faster processing without waiting for a pull request.
- **Disadvantages:** If the message rate is too high, it can **overload the server**.

---

# **Message Queue Acknowledgements & Pub/Sub Model**

## **Message Acknowledgements**

When a message queue dispatches a message to the application server, the **consumer (server)** must send an **acknowledgement (ACK)** after successfully processing the message.

- If the queue **does not receive an ACK** within a set time frame, it assumes the message **was not processed** and **resends it**.
- This mechanism ensures **reliable message delivery**, even if there are temporary server issues.
- This approach is similar to how **networking protocols** handle message delivery confirmation.

---

## **Publisher/Subscriber (Pub/Sub) Model**

The **Pub/Sub model** enables **decoupling** between publishers and subscribers, meaning they do **not need to be aware** of each other.

### **Benefits of the Pub/Sub Model**

- **Scalability:** Easily handles a growing number of publishers and subscribers.
- **Reliability:** Ensures messages **are not lost**, even if a subscriber is temporarily unavailable.
- **Flexibility:** New subscribers can be added without modifying existing publishers.

### **How It Works**

1. **Publisher dispatches messages** to a specific queue or topic.  
2. **One or more subscribers listen** to the queue or topic.  
3. **The message broker ensures delivery** of all messages to all subscribers of that topic.  
4. **Subscribers process messages independently** and at their own pace.  

---

## **Topics in the Pub/Sub Model**

- Publishers send messages to **specific topics** (categories for messages).  
- Subscribers indicate their interest by **subscribing to topics** they care about.  
- Multiple subscribers can **subscribe to the same topic** and receive the same messages.  

### **Example: Payment Processing**

Consider an **"OrderPlaced" topic** with multiple subscribers:

- **Inventory Service** updates stock levels.  
- **Billing Service** charges the customer.  
- **Shipping Service** prepares for delivery.  

Since all these services need to be **notified when an order is placed**, they subscribe to the same topic and process messages **independently**.

---

## **Expanding the System Without Changes**

One major advantage of the **Pub/Sub model** is that we can introduce **new subscribers** (e.g., a fraud detection service) without modifying the existing **publishing system**.  

This makes the architecture **highly adaptable** to future changes while maintaining efficiency and reliability.

