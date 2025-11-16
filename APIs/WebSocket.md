# Application Protocols Overview

There are several application-level protocols, each designed for specific use cases. Most of these protocols rely on **TCP** for communication, except **WebRTC**, which uses **UDP**. Below is a brief overview of some common protocols:

1. **FTP (File Transfer Protocol)**:
    - Used for transferring files between a client and a server.
2. **SMTP (Simple Mail Transfer Protocol)**:
    - Used for sending emails.
3. **SSH (Secure Shell)**:
    - Used for securely accessing and managing remote servers.
4. **HTTP/HTTPS (Hypertext Transfer Protocol)**:
    - Used for web browsing and follows a request-response model.
    - Stateless and unidirectional.
5. **WebSocket**:
    - Used for real-time, bidirectional communication.
    - Ideal for applications like chat, live streaming, and gaming.

---

### The Problem with HTTP for Real-Time Communication

When building a **real-time chat application**, HTTP has limitations:

- **Unidirectional**: HTTP follows a request-response model, where the client must initiate communication.
- **Polling Overhead**: To achieve real-time updates, the client must repeatedly poll the server for new data.
    - **Issues with Polling**:
        - **Too Frequent Polling**: Checking every second creates excessive requests, overloading the server.
        - **Too Infrequent Polling**: Checking every minute leads to delayed updates.

This makes HTTP suboptimal for real-time communication.

---

### WebSocket as the Solution

**WebSocket** is a protocol designed for **real-time, bidirectional communication**. It solves the limitations of HTTP by:

- Establishing a **persistent connection** between the client and server.
- Enabling **two-way communication** without the need for repeated polling.
- Being highly efficient for applications like:
    - **Chat applications**
    - **Live streaming**
    - **Real-time gaming**

---

### Establishing a WebSocket Connection

1. **Client Sends a WebSocket Handshake Request**:
    - The client initiates a WebSocket connection by sending an **HTTP Upgrade request** with special headers.
2. **Server Responds with a Handshake Response**:
    - If the server supports WebSocket, it responds with a **status code 101 (Switching Protocols)**.
    - This confirms the transition from HTTP to WebSocket.
3. **Data Transfer**:
    - After the handshake, the client and server can send data to each other in **real time**.
    - The connection remains open, eliminating the need for repeated requests.

---

### WebSocket Ports

- **WebSocket (WS)**: Uses port **80** (same as HTTP).
- **WebSocket Secure (WSS)**: Uses port **443** (same as HTTPS).

---

### Key Features of WebSocket

- **Bidirectional Communication**: Both client and server can send data at any time.
- **Efficient**: No need for repeated connections or polling.
- **Real-Time Updates**: Ideal for applications requiring instant data transfer.
- **Persistent Connection**: The connection remains open until explicitly closed.

---

### WebSocket vs. HTTP/2

- **HTTP/2** introduced **multiplexing**, allowing multiple requests over a single TCP connection.
- However, HTTP/2 is still **request-response-based** and does not replace WebSocket for real-time, bidirectional communication.

---

### Example: WebSocket in Action

### Use Case: Twitch Live Chat

- Twitch uses WebSocket for its **real-time chat** feature.
- This ensures that messages are delivered instantly without the need for polling.

### Proof of WebSocket Usage

- Open the **Developer Tools** in your browser.
- Go to the **Network** tab and filter for **WS** (WebSocket).
- You will see WebSocket connections being used for real-time chat.

### Example Status Code

- **101 Switching Protocols**: Indicates a successful WebSocket handshake.

---

### Summary of WebSocket

| **Feature** | **Description** |
| --- | --- |
| **Purpose** | Real-time, bidirectional communication. |
| **Use Cases** | Chat apps, live streaming, real-time gaming. |
| **Connection Type** | Persistent, bidirectional. |
| **Handshake** | Client sends an HTTP Upgrade request; server responds with status code 101. |
| **Ports** | WS: Port 80, WSS: Port 443. |
| **Advantages** | Efficient, real-time updates, no polling overhead. |
| **Limitations** | Requires network support (some firewalls may block WebSocket connections). |

---

### Key Takeaways

1. **WebSocket** is the best protocol for **real-time communication**.
2. It eliminates the need for **polling** by maintaining a **persistent, bidirectional connection**.
3. WebSocket is widely supported by browsers (Chrome, Firefox, Edge) and frameworks (Node.js, Django, [ASP.NET](http://asp.net/)).
4. It is ideal for applications like **chat**, **live streaming**, and **gaming**.