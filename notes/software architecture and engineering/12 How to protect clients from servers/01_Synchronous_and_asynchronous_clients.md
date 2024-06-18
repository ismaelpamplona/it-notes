# 1. Synchronous and asynchronous clients

Imagine you're calling a friend on the phone. Sometimes, you wait for them to pick up and talk right away. Other times, you leave a message and do other things until they call you back. Synchronous clients are like the first situation, and asynchronous clients are like the second.

### Synchronous Clients:

- When you make a request, you wait until you get an answer.
- It's like waiting in line at a store until it's your turn.

### Asynchronous Clients:

- You make a request and do other things while waiting for the answer.
- It's like placing an order online and doing your homework while waiting for the delivery.

### Admission Control Systems:

- These systems help manage traffic by controlling the number of requests.
- They use techniques like load shedding (dropping some requests) and rate limiting (slowing down the number of requests).

### Blocking I/O Clients (Synchronous):

- When you make a request, your application stops and waits for the response.
- This can lead to higher wait times if there are many requests.
- Example: Traditional phone call where you wait for the other person to answer.

### Non-Blocking I/O Clients (Asynchronous):

- When you make a request, your application continues to work on other tasks while waiting for the response.
- This is more efficient, especially when handling many requests.
- Example: Leaving a voicemail and continuing with your day until you get a callback.

### Key Differences:

1. **Simplicity:** Synchronous clients are easier to write, test, and debug.

2. **Latency:** Synchronous clients have lower latency with fewer concurrent requests.

3. **Throughput:** Asynchronous clients handle a larger number of concurrent requests better.

4. **Efficiency:** Asynchronous clients are better at managing traffic spikes.

5. **Resilience:** Asynchronous clients are more resilient to server issues and degraded performance.

### Important Industry Terms:

- **Admission Control:** Methods to manage the number of requests to a server.

- **Blocking I/O:** Waiting for a response before continuing with other tasks.

- **Non-Blocking I/O:** Continuing with other tasks while waiting for a response.

- **Latency:** The time it takes to get a response.

- **Throughput:** The number of requests handled in a given time period.

### Example in Software:

- **Synchronous Client:**

  ```mermaid
  sequenceDiagram
    participant User
    participant Server
    User->>Server: Send request
    Server-->>User: Send response
  ```

- **Asynchronous Client:**

  ```mermaid
  sequenceDiagram
  participant User
  participant Server
  User->>Server: Send request
  User->>User: Do other tasks
  Server-->>User: Send response
  ```

## Summary

Synchronous and asynchronous clients are different ways of making requests. Synchronous clients wait for a response, while asynchronous clients do other things while waiting. Admission control helps manage traffic, and understanding the difference between blocking and non-blocking I/O is crucial. Asynchronous clients are often more efficient and resilient in handling multiple requests and server issues.
