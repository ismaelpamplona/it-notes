# 2. Full and Empty Queue Problems

Imagine a queue as a line of people waiting for a roller coaster. Sometimes, the line is too long, and the roller coaster can't take more people (full queue). Other times, there are no people in line (empty queue). Handling these situations efficiently is crucial for smooth operations.

- **Load Shedding:** This is like the roller coaster deciding to let some people go without a ride if the line is too long. It's a way to prevent overload by dropping some requests.

- **Rate Limiting:** This is like controlling how many people can enter the line per minute. It prevents the line from getting too long too quickly by limiting the number of requests.

- **Failed Requests:** When the roller coaster can't take more people or there are other issues, you need a plan for what to do with those who can't get on. This involves handling requests that can't be processed.

- **Backpressure:** This is like slowing down the rate at which people join the line if it gets too long. It’s a way to signal upstream processes to slow down their request rate.

- **Elastic Scaling:** This is like adding more roller coasters when the line gets too long or reducing the number of roller coasters when there are fewer people. It helps handle varying loads by scaling resources up or down.

## Deep Dive and Important Points:

### Load Shedding:

1. **Definition:** Dropping some requests to prevent system overload.

2. **How it Works:**

   - If the queue is full, some incoming requests are rejected to maintain system stability.

     ```mermaid
      flowchart LR
          Start --> Decision{Queue Full?}
          Decision -->|Yes| Drop[Request Dropped]
          Decision -->|No| Process[Send Request to Service]
          Drop --> End
          Process --> End
     ```

   - The **Client** sends a request to the **Queue**.
   - If the **Queue** is full, the request is dropped, and the client is notified.

3. **Example:** An online ticket booking system that drops some requests during peak times to prevent overload.

### Rate Limiting:

1. **Definition:** Controlling the rate of incoming requests to prevent the queue from overloading.

2. **How it Works:**

   - Limits the number of requests per second or minute.

   ```mermaid
   sequenceDiagram
       participant Client
       participant RateLimiter
       participant Queue

       Client->>RateLimiter: Send Request
       RateLimiter->>Queue: Forward Request
       Note over RateLimiter: Limit Exceeded
       RateLimiter-->>Client: Request Denied
   ```

   - The **Client** sends a request to the **RateLimiter**.
   - If the rate limit is exceeded, the request is denied.

3. **Example:** An API that allows only a certain number of requests per minute to prevent abuse.

### What to do with Failed Requests:

1. **Definition:** Handling requests that cannot be processed.

2. **How it Works:**

   - Retrying, redirecting, or logging failed requests.

   ```mermaid
   sequenceDiagram
       participant Client
       participant Queue
       participant Service

       Client->>Queue: Send Request
       Queue->>Service: Process Request
       Service-->>Queue: Failed Response
       Queue-->>Client: Handle Failure
   ```

   - The **Client** sends a request to the **Queue**.
   - The **Service** fails to process the request, and the **Queue** handles the failure by retrying or notifying the client.

3. **Example:** A payment gateway that retries a failed transaction or notifies the user to try again later.

### Backpressure:

1. **Definition:** Slowing down the rate of incoming requests to prevent overload.

2. **How it Works:**

   - Signals upstream systems to reduce their request rate when the queue is full.

   ```mermaid
   sequenceDiagram
       participant Client
       participant Upstream
       participant Queue

       Client->>Upstream: Send Request
       Upstream->>Queue: Forward Request
       Note over Queue: Queue Full
       Queue-->>Upstream: Apply Backpressure
   ```

   - The **Queue** applies backpressure to the **Upstream** system, slowing down incoming requests.

3. **Example:** A video streaming service that reduces the rate of video uploads when the server is under heavy load.

### Elastic Scaling:

1. **Definition:** Dynamically adding or removing resources based on load.

2. **How it Works:**

   - Automatically scales up or down to handle varying loads.

     ```mermaid
     flowchart LR
         Start --> LoadBalancer[Check \n Load]
         LoadBalancer --> Decision{Is Load \n High?}
         Decision -->|Yes| ScaleUp[Scale Up \n Resources]
         Decision -->|No| ScaleDown[Scale Down \n Resources]
         ScaleUp --> End
         ScaleDown --> End
     ```

     - The **LoadBalancer** checks the **Queue** load and scales the **Service** up or down based on the current demand.

3. **Example:** A cloud-based service that adds more servers during peak usage times and reduces the number during low usage.

## Summary

Handling full and empty queue problems involves strategies like **load shedding** (dropping excess requests), **rate limiting** (controlling request rate), **handling failed requests** (retrying or redirecting), **backpressure** (slowing down request rate), and **elastic scaling** (adjusting resources based on load). These techniques help maintain system stability and performance under varying loads.
