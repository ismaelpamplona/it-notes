# 4. Blocking vs Non-blocking I/O

Imagine you're waiting in line for ice cream. Blocking I/O is like having to stay in line until it's your turn to get ice cream. Non-blocking I/O is like putting your name on a list, and you can play while you wait for your turn.

### Blocking I/O:

- When you make a request, you wait and do nothing else until the response comes back.
- It's like waiting in line and not moving until you get your ice cream.

### Non-blocking I/O:

- When you make a request, you can do other things while waiting for the response.
- It's like putting your name on a list and playing until your ice cream is ready.

## Deep Dive and Important Points:

### Sockets (Blocking and Non-blocking) and Connections:

1. **Blocking Sockets:**

   - **Definition:** Sockets that make the program wait until the data is sent or received.

   - **How it Works:**
     - The program pauses and waits for the operation to complete.

   ```mermaid
   sequenceDiagram
       participant Client
       participant Server

       Client->>Server: Request
       Server-->>Client: Response
       Note over Client: Client waits
   ```

   - The **Client** sends a request to the **Server** and waits for the response without doing anything else.

2. **Non-blocking Sockets:**

   - **Definition:** Sockets that allow the program to continue running while waiting for the data to be sent or received.

   - **How it Works:**
     - The program can perform other operations while waiting for the I/O operation to complete.

   ```mermaid
   sequenceDiagram
       participant Client
       participant Server

       Client->>Server: Request
       Note over Client: Client continues working
       Server-->>Client: Response
   ```

   - The **Client** sends a request to the **Server** and continues doing other tasks while waiting for the response.

### Thread per Connection Model:

1. **Definition:** Each connection gets its own dedicated thread.

2. **How it Works:**

   - When a client connects, a new thread is created to handle the connection.

   ```mermaid
   sequenceDiagram
       participant Client1
       participant Client2
       participant Server

       Client1->>Server: Connect
       activate Server
       Note over Server: Create Thread 1
       Client2->>Server: Connect
       activate Server
       Note over Server: Create Thread 2
   ```

   - **Client1** and **Client2** each get their own thread on the **Server** to handle their connections independently.

3. **Characteristics:**
   - **Isolation:** Each connection is isolated from others.
   - **Resource Intensive:** Requires a lot of resources for many connections.

### Thread per Request with Non-blocking I/O Model:

1. **Definition:** Each request within a connection is handled by a separate thread using non-blocking I/O.
2. **How it Works:**

   - A thread handles a request and uses non-blocking I/O to allow other operations while waiting.

   ```mermaid
   sequenceDiagram
       participant Client
       participant Server

       Client->>Server: Request 1
       activate Server
       Note over Server: Handle Request 1
       Client->>Server: Request 2
       activate Server
       Note over Server: Handle Request 2 using non-blocking I/O
   ```

   - The **Server** handles multiple requests from the **Client** using separate threads with non-blocking I/O.

3. **Characteristics:**
   - **Efficiency:** More efficient than thread per connection for handling multiple requests.
   - **Scalability:** Better scalability with non-blocking I/O.

### Event Loop Model:

1. **Definition:** A single thread runs an event loop that handles multiple I/O operations.

2. **How it Works:**

   - The event loop checks for I/O operations that are ready and processes them.

   ```mermaid
   sequenceDiagram
       participant Client1
       participant Client2
       participant Server

       Client1->>Server: Request 1
       Client2->>Server: Request 2
       activate Server
       Note over Server: Event Loop handles requests
       Server-->>Client1: Response 1
       Server-->>Client2: Response 2
   ```

   - The **Server** uses an event loop to handle requests from **Client1** and **Client2** efficiently.

3. **Characteristics:**
   - **Single Threaded:** Uses a single thread for multiple operations.
   - **Non-blocking:** Handles I/O operations without blocking the thread.

### Concurrency vs Parallelism:

1. **Concurrency:**

   - **Definition:** Handling multiple tasks at the same time by switching between them.

   - **Example:** Juggling tasks like checking emails and cooking dinner by switching between them.

   ```mermaid
   sequenceDiagram
       participant Task1
       participant Task2
       participant Processor

       Processor->>Task1: Start Task 1
       Processor-->>Task2: Switch to Task 2
       Processor-->>Task1: Switch back to Task 1
   ```

   - The **Processor** switches between **Task1** and **Task2** to handle them concurrently.

2. **Parallelism:**

   - **Definition:** Handling multiple tasks at the same time using multiple processors.

   - **Example:** Cooking dinner while someone else checks emails at the same time.

   ```mermaid
   sequenceDiagram
       participant Task1
       participant Task2
       participant Processor1
       participant Processor2

       Processor1->>Task1: Process Task 1
       Processor2-->>Task2: Process Task 2
   ```

   - **Processor1** handles **Task1** while **Processor2** handles **Task2** simultaneously.

## Summary

**Blocking I/O** makes the program wait for operations to complete, like standing in line. **Non-blocking I/O** allows the program to continue running while waiting, like playing while waiting for your turn. Models like **Thread per Connection** and **Event Loop** help manage how multiple I/O operations are handled efficiently. Understanding **Concurrency** (switching between tasks) and **Parallelism** (doing tasks at the same time) is crucial for optimizing performance in software systems.
