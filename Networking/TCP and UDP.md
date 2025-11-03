# TCP and UDP

**TCP (Transmission Control Protocol)** and **UDP (User Datagram Protocol)** are communication protocols used to manage how data packets are sent, received, and organized between devices over a network.

---

## **TCP (Transmission Control Protocol)**

**Key Features:**

1. **Reliability:**
    - Ensures all packets are delivered to the destination.
    - Resends lost packets to guarantee complete data transmission.
2. **Order:**
    - Reassembles packets in the exact order they were sent.
3. **Connection-Oriented:**
    - Establishes a connection between two devices using a **Three-Way Handshake** before data exchange.
4. **Acknowledgement:**
    - Requires confirmation (ACK) for every successfully received packet. If a packet is not acknowledged, TCP retransmits it.

**Drawbacks:**

- Slower than UDP due to higher overhead for reliability and order.

**Application Protocols:**

- **HTTP/HTTPS**: Web browsing.
- **SMTP**: Email communication.
- **WebSocket**: Persistent, two-way communication.

**Use Cases:**

- Email.
- Online messaging.

---

## **UDP (User Datagram Protocol)**

**Key Features:**

1. **Speed:**
    - Faster than TCP as it skips reliability checks and packet reordering.
2. **No Handshake:**
    - Does not establish a connection before transmitting data.
3. **Unreliable:**
    - Data packets may arrive out of order or may be lost entirely without retransmission.

**Advantages:**

- Efficient and low-latency communication.

**Use Cases:**

- **Live Streaming:** Video and audio streams prioritize real-time delivery over accuracy.
- **Online Gaming:** Ensures smooth gameplay by skipping dropped packets rather than waiting for retransmission.
- **DNS (Domain Name System):** Fast resolution of domain names to IP addresses.

---

## **Comparison: TCP vs. UDP**

| **Feature** | **TCP** | **UDP** |
| --- | --- | --- |
| **Reliability** | Ensures all packets are delivered. | No guarantee of delivery. |
| **Order** | Packets are reassembled in order. | Packets may arrive out of order. |
| **Connection** | Connection-oriented (Three-Way Handshake). | Connectionless. |
| **Speed** | Slower due to overhead. | Faster and lightweight. |
| **Use Cases** | Email, messaging, web browsing. | Live streaming, gaming, DNS. |

---

## **When to Use TCP vs. UDP**

- **TCP:** Use when reliability and order are essential (e.g., emails, file downloads, web browsing).
- **UDP:** Use when speed is more critical than reliability (e.g., live streaming, gaming, DNS).