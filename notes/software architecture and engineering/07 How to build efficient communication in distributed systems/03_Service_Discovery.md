# 3. Service Discovery

Imagine you have a large library with many sections and you need to find a specific book. Service discovery is like having a system that helps you find the exact location of the book you need quickly and efficiently. It allows services in a network to find each other and communicate without needing to know the exact location of other services beforehand.

## Server-Side Discovery Pattern

In server-side discovery, the client makes a request to a load balancer or a service gateway, which then forwards the request to the appropriate service instance.

### Pros:

- **Centralized Control:** The load balancer has a global view of all available service instances and can distribute traffic efficiently.
- **Simplified Clients:** Clients only need to know the address of the load balancer or service gateway, not the individual service instances.

### Cons:

- **Single Point of Failure:** The load balancer or gateway can become a bottleneck or a single point of failure if not properly managed.
- **Complexity:** Requires managing and maintaining the load balancer or service gateway infrastructure.

### Example:

- **Load Balancers:** Tools like NGINX, HAProxy, or AWS Elastic Load Balancing.

## Client-Side Discovery Pattern

In client-side discovery, the client is responsible for determining the network locations of available service instances and making requests directly to them.

### Pros:

- **No Central Bottleneck:** Eliminates the potential bottleneck of a load balancer or service gateway.
- **Scalability:** Can scale easily as clients discover and interact with service instances directly.

### Cons:

- **Complex Clients:** Clients need to implement discovery logic and be aware of the service registry.
- **Consistency Issues:** Ensuring all clients have an up-to-date view of available service instances can be challenging.

### Example:

- **Service Discovery Libraries:** Libraries like Netflix Eureka, Consul, or Zookeeper.

## Service Registry and Its Applications

A service registry is a database where service instances are registered and their locations are tracked. It acts as a central source of truth for service discovery.

### Applications:

1. **Service Registration:** Service instances register themselves with the service registry upon startup and deregister upon shutdown.

2. **Health Checks:** The registry performs regular health checks to ensure that registered instances are available and healthy.

3. **Service Discovery:** Clients or load balancers query the service registry to discover available service instances.

### Examples of Service Registries:

- **Consul:** Provides service discovery, health checking, and a KV store.
- **Eureka:** A REST-based service for locating services for the purpose of load balancing and failover.
- **Zookeeper:** A centralized service for maintaining configuration information, naming, and providing distributed synchronization.

### Summary:

- **Server-Side Discovery:**
  - Pros: Centralized control, simplified clients.
  - Cons: Single point of failure, complexity.
  - Example: NGINX, AWS ELB.
- **Client-Side Discovery:**

  - Pros: No central bottleneck, scalability.
  - Cons: Complex clients, consistency issues.
  - Example: Eureka, Consul.

- **Service Registry:**
  - Central database for service instances.
  - Applications: Service registration, health checks, service discovery.
  - Examples: Consul, Eureka, Zookeeper.
