# **Domain Name System (DNS)**

The **Domain Name System (DNS)** functions as the internet’s **phone book**, translating human-readable **domain names** into numerical **IP addresses** that computers understand.

## **How DNS Works**

1. When you enter a domain name (e.g., `google.com`) into your browser, DNS translates it into an **IP address** (e.g., `142.251.211.238`).
2. This IP address allows your device to locate and connect to the correct **server** that hosts the website.
3. DNS caching speeds up access by storing frequently used IP addresses.

## **Organizations Involved in DNS Management**

### **1. ICANN (Internet Corporation for Assigned Names and Numbers)**

- A **non-profit organization** that oversees **domain name assignments** and DNS infrastructure.
- Ensures the **coordination, security, and operation** of domain names.

### **2. Domain Name Registrars**

- Companies authorized by ICANN to sell and **register domain names**.
- Examples: **GoDaddy, Google Domains, HostGator**.
- Act as intermediaries for users to purchase domain names.

### **3. Internet Service Providers (ISPs)**

- Facilitate communication between **users, domain registrars, and ICANN**.
- Manage **DNS resolution** for customers, helping translate domain names into IP addresses.

## **DNS Records**

DNS records store information related to a domain. Some common types:

- **A (Address) Record**: Maps a domain to an IPv4 address (e.g., `neetcode.io` → `192.158.1.39`).
- **Caching**: Devices store DNS records to reduce lookup times for frequently visited websites.

---

# **Client-Server-DNS Connection**

1. **Client** requests a domain (e.g., `neetcode.io`).
2. **DNS server** retrieves the domain’s IP address.
3. The request is forwarded to the **server** hosting the website.
4. The **server responds** with the requested webpage.

A **server**:

- Has a **public IP address** and a **domain name**.
- Uses **firewalls** for security.
- Handles **incoming requests** from users.

---

# **Anatomy of a URL (Uniform Resource Locator)**


Example:

**`https://domains.google.com/get-started`**

### **1. Protocol (Scheme)**

- Defines the communication method used.
- **Common protocols:**
    - `http://` (Hypertext Transfer Protocol)
    - `https://` (Secure HTTP)
    - `ftp://` (File Transfer Protocol)
    - `ssh://` (Secure Shell for remote login)

**Example URLs:**

- FTP: `ftp://ftp.example.com/pub/file.txt`
- SSH: `ssh://username@example.com:22`

### **2. Domain Structure**

- **Subdomain:** `domains` (specific section of the website).
- **Primary Domain:** `google.com` (core identity of the website).
- **Top-Level Domain (TLD):** `.com` (indicates the domain category, e.g., `.io` for tech companies).

### **3. Path**

- Represents a **specific location** within the website.
- Example: `/get-started` directs users to a specific section.

### **4. Ports**

- Standard ports:
    - **HTTP:** Port **80**
    - **HTTPS:** Port **443**
- Custom ports must be specified, e.g., `localhost:8080`.

---

# **DNS Summary**

- **Maps** domain names to **IP addresses** for easier web access.
- Managed by **ICANN**, **registrars**, and **ISPs**.
- Uses **DNS records** to store mapping information.
- URLs are structured with **protocols, domains, paths, and ports**.