### **API Design Overview**

API design focuses on how users interact with a server and its resources. It defines the **surface area** (what users can interact with) and ensures consistency, usability, and backward compatibility.

---

### **Key Concepts**

1. **CRUD Operations**:
    - APIs typically support **Create, Read, Update, Delete (CRUD)** operations.
    - These map to HTTP methods:
        - **GET**: Retrieve data (e.g., fetch tweets).
        - **POST**: Create data (e.g., create a tweet).
        - **PUT/PATCH**: Update data (e.g., edit a tweet).
        - **DELETE**: Remove data (e.g., delete a tweet).
2. **Entities (Resources)**:
    - Resources are the objects or nouns being manipulated (e.g., tweets, users).
    - Each resource has attributes (e.g., `userId`, `tweetId`, `content`, `createdAt`, `likes`).
3. **API Endpoints**:
    - Endpoints are URLs that represent resources and actions.
4. **Versioning**:
    - APIs are versioned to manage changes (e.g., `v1.0`, `v2.0`).
    - Older versions are deprecated to encourage migration to newer versions.
5. **Pagination**:
    - Used for retrieving large datasets (e.g., tweets).
    - Parameters like `limit` and `offset` control the number of results returned.


**1. Creating a Tweet**

- **Endpoint**: `POST <https://api.twitter.com/v1.0/tweet`>
- **Parameters**:
    - `userId`: The creator of the tweet (required).
    - `content`: The tweet text (required).
    - `parentId`: Optional, for replies.
- **Response**:
    - Returns the created tweet object with attributes like `tweetId`, `createdAt`, and `likes`.

### **2. Retrieving Tweets**

- **Single Tweet**:
    - **Endpoint**: `GET <https://api.twitter.com/v1.0/tweet/:tweetId`>
    - Fetches a specific tweet by its ID.
- **Multiple Tweets**:
    - **Endpoint**: `GET <https://api.twitter.com/v1.0/users/:userId/tweets?limit=10&offset=0`>
    - Uses pagination (`limit` and `offset`) to fetch a subset of tweets.

### **3. Updating a Tweet**

- **Endpoint**: `PUT <https://api.twitter.com/v1.0/tweet/:tweetId`>
- **Parameters**:
    - `content`: Updated tweet text.
- **Response**:
    - Returns the updated tweet object.

### **4. Deleting a Tweet**

- **Endpoint**: `DELETE <https://api.twitter.com/v1.0/tweet/:tweetId`>
- **Response**:
    - Confirms deletion.

---

### **Best Practices**

1. **Backward Compatibility**:
    - Avoid breaking changes by making new parameters optional (e.g., `parentId` in `createTweet`).
2. **Idempotency**:
    - Ensure GET requests are idempotent (no side effects, same response for repeated calls).
3. **Error Handling**:
    - Use appropriate HTTP status codes (e.g., `200` for success, `400` for bad requests, `404` for not found).
4. **Security**:
    - Use API keys or tokens to authenticate requests.
5. **Documentation**:
    - Provide clear documentation for endpoints, parameters, and responses.

---

### **Example API Calls**

### **Create a Tweet**

```
POST <https://api.twitter.com/v1.0/tweet>
Payload:
{
  "userId": "123",
  "content": "Hello, Twitter!",
  "parentId": "456"  // Optional
}
Response:
{
  "tweetId": "789",
  "userId": "123",
  "content": "Hello, Twitter!",
  "createdAt": "2023-10-01T12:00:00Z",
  "likes": 0
}

```

### **Fetch Tweets**

```
GET <https://api.twitter.com/v1.0/users/123/tweets?limit=10&offset=0>
Response:
{
  "tweets": [
    {
      "tweetId": "789",
      "userId": "123",
      "content": "Hello, Twitter!",
      "createdAt": "2023-10-01T12:00:00Z",
      "likes": 0
    },
    ...
  ]
}

```

### **Delete a Tweet**

```
DELETE <https://api.twitter.com/v1.0/tweet/789>
Response:
{
  "message": "Tweet deleted successfully."
}

```

---

### **Why Good API Design Matters**

- **Public-Facing**: APIs are used by many applications, so changes must be carefully managed.
- **Consistency**: Clear and consistent APIs reduce integration effort.
- **Scalability**: Well-designed APIs handle growth and new features gracefully.