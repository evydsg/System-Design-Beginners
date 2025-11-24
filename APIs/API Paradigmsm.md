# Application Programming Interface

## Definition

An API (Application Programming Interface) is a set of rules and protocols that allow software applications to communicate with each other. APIs enable applications to access functionality and data from other systems in a structured manner.

### Key Characteristics:

- APIs allow applications to interact with local storage or remote services.
- APIs define objects and functions that an application can call.
- APIs serve user requests by retrieving or modifying data.

## Types of APIs

### REST (REpresentational State Transfer)

- **Standards API**: REST APIs follow a set of universal standards that are widely used.
- **Built on HTTP**: REST APIs leverage standard HTTP methods such as GET, POST, PUT, and DELETE.
- **Stateless**: Each request carries all necessary information; the server does not store session data.
- **Response Codes**: Common HTTP status codes include:
    - `200 OK` (Success)
    - `201 Created`
    - `202 Accepted`
- **Pagination**:
    - Helps manage large data sets efficiently.
    - Requests include parameters (e.g., `offset=10&limit=10`) to fetch only a subset of data.
- **Data Format**:
    - JSON (JavaScript Object Notation) is the preferred format.
    - JSON is human-readable and follows key-value pair structures.

![image.png](attachment:9dd6fbad-64e1-4f08-ae71-580e1c6ef273:image.png)

### GraphQL

- **Created by Facebook** to address limitations of REST.
- **Built on HTTP**: Uses only `POST` requests.
- **Query-based**:
    - Clients define exactly what data they need.
    - Solves issues of **over-fetching** (getting unnecessary data) and **under-fetching** (making multiple requests for missing data).
- **Example Query**:
    
    ```graphql
    {
      launchesPast(limit: 10) {
        mission_name
        launch_date_local
        launch_site {
          site_name_long
        }
        links {
          article_link
          video_link
        }
        rocket {
          rocket_name
        }
      }
    }
    ```
    

### gRPC (gRPC Remote Procedure Call)

- **Developed by Google** for efficient, high-performance APIs.
- **Built on HTTP/2**: Allows multiplexed streams and lower latency.
- **Uses Protocol Buffers (protobufs)**:
    - Binary serialization format for smaller and faster data transfer.
    - Requires defining schemas.
- **Supports streaming**:
    - Real-time bidirectional communication.
    - Ideal for server-to-server interactions.
- **Error Handling**:
    - Unlike REST, gRPC does not use HTTP status codes; developers define custom error messages.

### Example gRPC API Definition

```
syntax = "proto3";

service Greeter {
  rpc SayHello (HelloRequest) returns (HelloReply) {}
  rpc SayHelloAgain (HelloRequest) returns (HelloReply) {}
}

message HelloRequest {
  string name = 1;
}

message HelloReply {
  string message = 1;
}
```

## API Paradigms

1. **REST** - Best for web-based applications requiring standard HTTP methods.
2. **GraphQL** - Useful when precise data fetching is needed to reduce unnecessary data transfer.
3. **gRPC** - Ideal for microservices, high-speed communication, and streaming scenarios.

## Limitations of REST

- **Over-fetching**: Clients receive more data than necessary, leading to inefficiencies.
- **Under-fetching**: Clients must make multiple requests to gather all required information.

## Advantages of GraphQL

- **Efficient Data Fetching**: Clients request only the required fields.
- **Single Endpoint**: Reduces complexity compared to multiple REST endpoints.

## Advantages of gRPC

- **Performance**: Faster than REST due to binary serialization.
- **Streaming Support**: Ideal for real-time applications.
- **Efficient Error Handling**: Custom error messages for better debugging.