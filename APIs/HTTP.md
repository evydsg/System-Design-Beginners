# HTTP

# Application Protocols

## Client-Server Model

- **Client**:
    - An application or system that accesses services provided by a server.
    - Can be a web browser, email software, mobile app, or any software needing services.
    - Initiates communication by sending requests to the server.
    - Often referred to as the "caller."
- **Server**:
    - A computer, device, or software that provides resources, data, or services to clients.
    - Waits for incoming requests and responds by fulfilling them.
    - Examples: web servers, email servers, database servers.
    - Often referred to as the "callee."
- **Roles**:
    - A single machine can act as both a client and a server.
    - In peer-to-peer (P2P) networks, machines can simultaneously function as clients and servers.

---

## RPC (Remote Procedure Call)

- **Definition**:
    - Allows a program to execute functions on a separate machine over a network.
    - Commonly used in distributed systems where tasks are managed across multiple computers.
- **Example**:
    - When searching for "NeetCode" on YouTube, the browser calls a function like `listVideos('neetcode')` on YouTube's servers to retrieve the video list.

---

## HTTP (Hypertext Transfer Protocol)

- **Overview**:
    - Built on top of IP and TCP.
    - A request/response protocol used for transmitting data over the web.
    - Developers have control over HTTP in web applications.
- **Key Components**:
    - **Request Method**:
        - **GET**: Retrieves a resource (idempotent).
        - **POST**: Sends data to create a new resource (not idempotent).
        - **PUT**: Updates a resource (idempotent).
        - **DELETE**: Deletes a resource (idempotent).
    - **Endpoint**: URL + Method.
    - **Path**: Specific location of the resource.
    - **Status Codes**:
        - **Informational (100-199)**: Request received and being processed.
        - **Successful (200-299)**: Request succeeded (e.g., 200 OK, 201 Created).
        - **Redirection (300-399)**: Resource moved or temporarily available elsewhere.
        - **Client Error (400-499)**: Invalid request (e.g., 400 Bad Request, 401 Unauthorized, 404 Not Found).
        - **Server Error (500-599)**: Server failed to fulfill the request (e.g., 500 Internal Server Error, 502 Bad Gateway).
- **Anatomy of an HTTP Request**:
    - **Request Method**: Desired action (e.g., GET, POST).
    - **Request URL/URI**: Specifies where the request is sent.
    - **Headers**: Provide additional information (e.g., content type, cookies).
    - **Body**: Contains data for methods like POST or PUT (not used in GET).

---

## SSL/TLS (Secure Sockets Layer / Transport Layer Security)

- **Purpose**:
    - Encrypts data transmitted over the network to prevent attacks like Man-in-the-Middle (MITM).
    - HTTP alone is insecure, but HTTPS (HTTP + TLS) ensures secure communication.
- **Key Points**:
    - TLS is the modern version of SSL.
    - HTTPS is the combination of HTTP and TLS, making it the standard for secure web communication.

---

## HTTP Strict Transport Security (HSTS)

- **Purpose**:
    - Ensures that browsers automatically upgrade HTTP requests to HTTPS for enhanced security.
    - Once a browser receives the HSTS policy via an HTTPS response header, it enforces HTTPS for all subsequent requests.

---

## Developer Tools: Network Tab

- **Purpose**:
    - Monitors all network requests made by the browser.
    - Provides details like request name, status code, request type, response size, and time taken.
- **Key Features**:
    - **Request Headers**: Information about the request (e.g., method, content type).
    - **Response Headers**: Information about the server's response (e.g., cookies, caching behavior).
    - **Body**: Data sent or received (e.g., payload in POST requests).

---

## Summary

- **Client-Server Model**: Clients request services, and servers fulfill those requests.
- **RPC**: Enables remote execution of functions over a network.
- **HTTP**: The core protocol of the web, with methods like GET, POST, PUT, and DELETE.
- **SSL/TLS**: Ensures secure communication by encrypting data.
- **HTTPS**: The secure version of HTTP, combining HTTP with TLS.