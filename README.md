# Reflection

### 1. RPC Methods: Unary vs. Streaming
**Question:** What are the key differences between unary, server streaming, and bi-directional streaming RPC methods, and in what scenarios would each be most suitable?

> **Answer:**
> The key differences is how the data are sent or got. Unary only allows client sends a single request which then after waiting the server sends a single respond. Server streaming is when client sends a single request but the server sends a big respond that can be continuously. Bidirection allows both client and server can send multiple messages to each other in a continuous stream. Unary best scenarios happend when you dealing with high concurrent loads like Financial Data Feeds. Server streaming best scenarios when you are doing Log Monitoring. Bidirection best scenarios when you dealing something collaborating like Google Docs.


---

### 2. Security in Rust gRPC
**Question:** What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?

> **Answer:**
> gRPC traffic is unencrypted so securing the transport layer is a must.We can do this by enabling TLS/SSL via feature flags in Tonic (like `tls-ring`). For authentication, gRPC use Metadata for clients to attach their tokens. We can validate this tokens securely by using Tonic `Interceptor`. Once the `Interceptor` has verified the user's identity, we can give the access controls by using actual service handler like `tonic-middleware` crate.

---

### 3. Challenges of Bidirectional Streaming
**Question:** What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?

> **Answer:**
> Deadlocks. This happend because Bidirectional allows both client and server to send and receive concurrently. If happens a poor synchronization, then this problem comes up. But this shouldn't be a problem because of Rust. Other problem can occur that is immediate connection termination when the stream got error. This is different from unary when it got errors because in unary it only returned as discrete response.

---

### 4. `ReceiverStream` in Tonic/Tokio
**Question:** What are the advantages and disadvantages of using the `tokio_stream::wrappers::ReceiverStream` for streaming responses in Rust gRPC services?

> **Answer:**
> Natural Backpressure Management, the bounded channel given by this library, it automatically protect the server from resource exhaustion. On the other hand: Task Spawning Overhead. Using this library requires to allocate and spawn a new Tokio task just to feed the channel which cause context-switching overhead and allocation costs.

---

### 5. Code Structure and Modularity
**Question:** In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?

> **Answer:**
> [Enter your answer here]

---

### 6. Complex Logic: `MyPaymentService`
**Question:** In the `MyPaymentService` implementation, what additional steps might be necessary to handle more complex payment processing logic?

> **Answer:**
> [Enter your answer here]

---

### 7. Architectural Impact of gRPC
**Question:** What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?

> **Answer:**
> [Enter your answer here]

---

### 8. HTTP/2 vs. HTTP/1.1 & WebSockets
**Question:** What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?

> **Answer:**
> [Enter your answer here]

---

### 9. Real-time Communication: REST vs. gRPC
**Question:** How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?

> **Answer:**
> [Enter your answer here]

---

### 10. Protobuf vs. JSON Payloads
**Question:** What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?

> **Answer:**
> [Enter your answer here]