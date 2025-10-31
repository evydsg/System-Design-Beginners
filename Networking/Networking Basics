# Networking Basics: A Developer's Guide


## How Do Machines Communicate?

- **IP Address**: Machines use IP addresses to identify and communicate with each other.
    - **IPv4** (32-bit): Supports up to ~4 billion addresses.
    
    - **IPv6** (128-bit): Provides a much larger address space to accommodate the growing number of devices.
- **Communication Process**:
    - Data is sent in packets, which include:
        - **IP Header**: Contains source and destination addresses (network layer).
        - **TCP Header**: Ensures data arrives in the correct order (transport layer).
            - Includes metadata like sequence numbers for reassembly.
        - **Application Data**: Contains information like HTTP or HTTPS requests (application layer).

---

## Types of IP Addresses

1. **Public IP**:
    - Globally unique.
    - Assigned to your router by your Internet Service Provider (ISP).
    - Routers assign **private IP addresses** to individual devices within the network.
2. **Private IP**:
    - Used within local networks (e.g., home or office).
    - Not accessible from the broader internet.
3. **Static IP**:
    - Fixed and does not change.
    - Commonly used by servers.
4. **Dynamic IP**:
    - Changes over time, usually assigned automatically by ISPs.
    - Suitable for clients due to flexibility and easier management.

---

## Ports: Identifying Applications on a Device

- **What Are Ports?**
    - Numeric identifiers (16-bit) for applications or services on a device.
    - Range: **0–65,535**.
    - Example:
        - Port **80**: HTTP traffic.
        - Port **4200**: Default for Angular applications.
- **Key Rule**:
    - Each application must use a unique port.
    - Two applications cannot run on the same port simultaneously.

---

## How Data is Transferred Over a Network

Imagine two devices, **Alice** (client) and **Bob** (server), exchanging information:

1. **Sending Data**:
    - Data is divided into **packets**.
    - Each packet includes:
        - **IP Header**: Acts like the "To" and "From" address on an envelope.
        - **TCP Header**: Ensures packets arrive in the right order.
        - **Payload (Application Data)**: The actual message or content.
2. **Reassembling Data**:
    - If packets arrive out of order, the TCP sequence numbers help reassemble them correctly.
    - Similar to receiving numbered pages in a letter.

---

## Network Layers: How Everything Fits Together

- **Application Layer** (e.g., HTTP/HTTPS): Handles user interactions and application data.
- **Transport Layer** (e.g., TCP): Ensures reliable data delivery.
- **Network Layer** (e.g., IP): Determines the route for data transmission.

---

## Public vs. Private Networks

- **Public Network**:
    - Devices communicate globally using public IP addresses.
    - Examples: Accessing websites, sending emails.
- **Private Network**:
    - Devices within a local network use private IP addresses.
    - Examples: Sharing files within an office.

---

## Static vs. Dynamic IP Addresses

- **Static IP**:
    - Permanent and manually configured.
    - Often used by servers for consistent accessibility.
- **Dynamic IP**:
    - Automatically assigned and changes over time.
    - More common for clients due to flexibility.