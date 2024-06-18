# Summary of Key Topics in Distributed Systems

## 1. Replication

Replication involves creating copies of data across multiple servers or locations to ensure data availability, fault tolerance, and improved performance.

**Types of Replication:**

- **Master-Slave Replication:** One master server handles writes and propagates changes to one or more slave servers that handle reads.
- **Multi-Master Replication:** Multiple servers can handle writes, and changes are propagated to all servers.

**Consistency Models:**

- **Strong Consistency:** All copies of the data are updated immediately.
- **Eventual Consistency:** Updates are propagated gradually, and all copies will be consistent eventually.

**Use Cases:**

- Disaster recovery.
- Load balancing read requests.
- Geographically distributed applications.

## 2. Coordination Services

Coordination services manage distributed systems by providing mechanisms for synchronization, configuration management, and leader election

**Key Features:**

- **Configuration Management:** Maintaining configuration information and providing it to nodes.
- **Leader Election:** Choosing a leader among distributed nodes to coordinate tasks.
- **Distributed Locks:** Ensuring that only one node accesses a resource at a time.

**Examples:**

- Apache ZooKeeper: Manages configuration and coordination of distributed applications.
- etcd: A distributed key-value store used for configuration management.

## 3. Load Balancing

Load balancing distributes incoming network traffic across multiple servers to ensure no single server becomes overwhelmed, thus improving system performance and availability.

**Load Balancing Algorithms:**

- **Round-Robin:** Distributes requests sequentially across servers.
- **Least Connections:** Directs requests to the server with the fewest active connections.
- **IP Hash:** Distributes requests based on the client’s IP address.

**Types of Load Balancers:**

- **Hardware Load Balancers:** Physical devices designed for load balancing.
- **Software Load Balancers:** Applications or services like Nginx, HAProxy.

**Use Cases:**

- Distributing web traffic.
- Balancing database queries.
- Ensuring high availability.

## 4. Batch Processing

Batch processing involves processing large volumes of data in groups or batches at scheduled times, suitable for scenarios where real-time processing is not required

**Characteristics:**

- Processes large volumes of data.
- Executes jobs without manual intervention.
- Suitable for tasks like ETL (Extract, Transform, Load), data analysis.

**Tools:**

- Apache Hadoop: Framework for distributed storage and processing.
- Apache Spark: Unified analytics engine for large-scale data processing.

**Use Cases:**

- Processing log files.
- Generating reports.
- Data warehousing.

## 5. Consistency

Consistency ensures that all nodes in a distributed system have the same data at any given time.

**Consistency Models:**

- **Strong Consistency:** Immediate synchronization of data across all nodes.
- **Eventual Consistency:** Data changes are propagated gradually, and all nodes become consistent eventually.
- **Causal Consistency:** Ensures that causally related operations are seen in the same order by all nodes.

**Use Cases:**

- Financial transactions.
- Social media updates.
- Distributed databases.

## 6. Reverse Proxy

A reverse proxy sits between clients and backend servers, forwarding client requests to the appropriate server. It enhances security, load balancing, and caching

**Functions:**

- Distributes client requests to multiple backend servers.
- Acts as a security barrier, hiding backend servers from clients.
- Can cache responses to improve performance.

**Examples:**

- Nginx: High-performance reverse proxy and web server.
- HAProxy: Reliable, high-performance TCP/HTTP load balancer.

**Use Cases:**

- Distributing load across servers.
- Protecting backend servers.
- Implementing SSL termination.

## 7. Caching

Caching involves storing copies of frequently accessed data to reduce latency and improve performance.

**Types of Caching:**

- **In-Memory Caching:** Stores data in RAM for fast access (e.g., Redis, Memcached).
- **Disk Caching:** Stores data on disk for persistence.
- **CDN Caching:** Distributes cached content across multiple geographical locations.

**Caching Strategies:**

- **Write-Through:** Data is written to the cache and the backing store at the same time.
- **Write-Back:** Data is written to the cache and later written to the backing store.
- **Write-Around:** Data is written directly to the backing store, bypassing the cache.

**Use Cases:**

- Accelerating web applications.
- Reducing database load.
- Improving response times for frequently accessed data.

## 8. Stream Processing

Stream processing involves continuous, real-time processing of data streams, enabling real-time analytics, monitoring, and event detection

**Characteristics:**

- Processes data in real-time as it arrives.
- Suitable for time-sensitive applications.
- Provides immediate insights and responses.

**Tools:**

- Apache Kafka: Distributed event streaming platform.
- Apache Flink: Stream processing framework.
- Apache Storm: Real-time computation system.

**Use Cases:**

- Real-time analytics.
- Monitoring and alerting systems.
- Fraud detection.

## 9. CAP Theorem

The CAP theorem states that in a distributed system, it is impossible to simultaneously achieve Consistency, Availability, and Partition Tolerance. Systems must choose two of the three properties.

**Components:**

- **Consistency:** All nodes see the same data at the same time.
- **Availability:** Every request receives a response, either successful or failed.
- **Partition Tolerance:** The system continues to operate despite network partitions.

**Implications:**

- Trade-offs are necessary; a system can be CA, CP, or AP but not all three.

**Use Cases:**

- Designing distributed databases.
- Choosing trade-offs based on application requirements.

## 10. API Gateway

An API gateway acts as a single entry point for multiple microservices, handling requests, routing, authentication, and rate limiting

**Functions:**

- Centralized request routing.
- Authentication and authorization.
- Rate limiting and throttling.

**Examples:**

- Kong: Open-source API gateway and microservices management layer.
- AWS API Gateway: Fully managed service for creating, deploying, and managing APIs.

**Use Cases:**

- Simplifying client interactions with microservices.
- Securing APIs.
- Managing traffic and rate limiting.

## 11. SQL and NoSQL Databases

SQL and NoSQL databases are used for storing and retrieving data, each with different characteristics and use cases.

**SQL Databases:**

- Relational and use structured query language (SQL).
- Strong consistency and ACID transactions.
- Examples: MySQL, PostgreSQL, Oracle.

**NoSQL Databases:**

- Non-relational and designed for flexible schemas.
- Can handle large volumes of unstructured data.
- Examples: MongoDB, Cassandra, Redis.

**Use Cases:**

- SQL: Traditional applications, financial systems.
- NoSQL: Big data applications, real-time analytics, flexible schema requirements.

## 12. Cell-based Architecture

Cell-based architecture divides a system into smaller, isolated units called cells. Each cell operates independently, improving fault isolation, scalability, and manageability

**Characteristics:**

- Each cell is a self-contained unit with its own resources.
- Cells can be scaled independently based on demand.
- Faults are contained within a cell, preventing widespread failures.

**Use Cases:**

- Large-scale distributed systems.
- Cloud-native applications.
- Microservices architectures.

## 13. Leader Election

Leader election is a process in distributed systems to designate a single node as the coordinator or leader among multiple nodes. It is crucial for coordination and consistency.

**Algorithms:**

- **Bully Algorithm:** Nodes with higher IDs have priority in becoming the leader.
- **Raft Algorithm:** Consensus algorithm for distributed systems.
- **Paxos Algorithm:** Ensures consensus in a network of unreliable processors.

**Use Cases:**

- Managing distributed locks.
- Coordinating tasks in distributed systems.
- Ensuring consistency in distributed databases.

## 14. API Design (REST and RPC)

REST (Representational State Transfer) and RPC (Remote Procedure Call) are two common API design styles, each with its own use cases and trade-offs

**REST:**

- Uses HTTP methods (GET, POST, PUT, DELETE).
- Stateless communication.
- Uses URIs to represent resources.

**RPC:**

- Calls methods on remote services.
- Can be more efficient for certain use cases.
- Examples: gRPC, JSON-RPC.

**Use Cases:**

- REST: Web services, CRUD operations.
- RPC: High-performance services, internal service communication.

## 15. Other Data Stores

Other specialized data stores include time-series databases, graph databases, and key-value stores, each optimized for specific use cases.

**Types:**

- **Time-Series Databases:** Optimized for time-stamped data (e.g., InfluxDB).
- **Graph Databases:** Optimized for relationships and connections (e.g., Neo4j).
- **Key-Value Stores:** Simple storage for key-value pairs (e.g., Redis).

**Use Cases:**

- Time-series: Monitoring, IoT data.
- Graph: Social networks, recommendation systems.
- Key-value: Caching, session management.

## 16. Important Data Structures

Key data structures in distributed systems include hash tables, distributed hash tables (DHT), trees, graphs, and queues, essential for efficient data storage, retrieval, and processing

- **Hash Tables:** Key-value storage with fast lookups.
- **Distributed Hash Tables (DHT):** Decentralized key-value storage for distributed systems.
- **Trees:** Hierarchical data structure (e.g., B-trees, binary trees).
- **Graphs:** Nodes and edges representing relationships.
- **Queues:** FIFO data structure for task scheduling.
