# 10. Push and Pull Technologies in Real-Life Systems

When designing systems, it's essential to select the appropriate technology based on the specific requirements and constraints. Here are some examples of push and pull technologies used in various real-life systems:

## Messaging Systems

### AWS SQS (Simple Queue Service)

- **Type:** Pull-based
- **Polling Methods:** Short Polling, Long Polling
- **Use Case:** Suitable for decoupling components in a distributed system, where messages are pulled from the queue by consumers.

### Apache Kafka

- **Type:** Pull-based
- **Polling Methods:** Short Polling, Long Polling
- **Use Case:** Ideal for building real-time data pipelines and streaming applications, where consumers pull data from topics.

### AWS Kinesis

- **Type:** Pull-based
- **Polling Method:** Short Polling
- **Use Case:** Designed for real-time processing of streaming data, where data records are pulled from Kinesis streams.

### RabbitMQ

- **Type:** Push-based
- **Use Case:** Used for real-time messaging between components, where messages are pushed to consumers as they become available.

### Apache ActiveMQ

- **Type:** Push-based
- **Use Case:** Suitable for enterprise messaging, where messages are pushed to consumers, ensuring reliable delivery and support for various messaging protocols.

## Real-Life Application Scenarios

### Online Chat

- **WebSocket:** For real-time, bidirectional communication between server and client.
- **Long Polling:** An alternative for environments where WebSocket is not supported.
- **Server-Sent Events (SSE):** For real-time updates from server to client, especially for older browsers.
- **HTTP Post Requests:** For sending messages (write operations).

### News Feed

- **Short Polling:** Periodic requests for updates.
- **Long Polling:** Reduces the number of requests by keeping the connection open until new data is available.
- **WebSocket:** Real-time updates with minimal latency.
- **SSE:** Continuous updates from the server to the client.

### Stock Tracking App

- **WebSocket:** Real-time updates for stock prices and transactions.
- **SSE:** Suitable for continuous updates to clients.

### Browser Game

- **WebSocket:** For real-time interaction between players and the game server.

### Collaborative Code Editor

- **Long Polling:** Ensures that updates are sent as soon as they are available.
- **WebSocket:** Real-time, bidirectional communication for seamless collaboration.
- **SSE:** Server-to-client updates for changes in the code.

## Summary of Technology Choices

### Push-Based Technologies

- **WebSocket:** Best for real-time, bidirectional communication with low latency.
- **SSE:** Suitable for server-to-client updates where WebSocket might be overkill or not supported.
- **RabbitMQ:** Ideal for real-time messaging with reliable delivery.
- **Apache ActiveMQ:** Enterprise messaging with support for various protocols.

### Pull-Based Technologies

- **AWS SQS:** Decoupling components in distributed systems.
- **Apache Kafka:** Real-time data pipelines and streaming.
- **AWS Kinesis:** Real-time processing of streaming data.
- **Short Polling:** Simple implementation but less efficient.
- **Long Polling:** More efficient than short polling, reduces server load and latency.
