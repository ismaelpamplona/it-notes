# 6. Consistent Hashing

Imagine you have a circular table, and you want to distribute candies evenly among your friends seated around the table. Consistent hashing is like placing the candies at equal distances around the table so that each friend gets a fair share. In software, consistent hashing helps distribute data across servers in a balanced way, even when servers are added or removed.

Consistent hashing is a way to distribute data (like candies) evenly across multiple servers (friends) in a way that handles changes smoothly. For example:

- When a new friend joins or leaves the table, the candies are redistributed evenly without too much disruption.

1. **How to Implement Consistent Hashing:**

   - **Hash Function:**

     - Use a hash function to assign each data item a position on a circular hash space (like a ring).
     - Example: Hash(data) % 360 (for a circular space of 360 degrees).

   - **Server Placement:**

     - Each server is also assigned a position on the circular hash space using the same hash function.
     - Example: Hash(server1) % 360.

   - **Data Assignment:**

     - Each data item is assigned to the nearest server in the clockwise direction on the hash ring.
     - Example: Data with hash value 120 is assigned to the server with hash value closest to 120 in the clockwise direction.

   - **Rebalancing:** When a server is added or removed, only a small portion of the data needs to be reassigned, minimizing disruption.

2. **Advantages and Disadvantages of Consistent Hashing:**

   - **Advantages:**

     - **Scalability:** Easily handles adding or removing servers with minimal data movement.
     - **Even Distribution:** Distributes data evenly across servers.
     - **Fault Tolerance:** If a server fails, only the data on that server needs to be redistributed.

   - **Disadvantages:**
     - **Complexity:** More complex to implement compared to simple hashing.
     - **Hash Collisions:** Can still suffer from hash collisions if not managed properly.

3. **Virtual Nodes:**

   - Virtual nodes (or vnodes) are additional positions on the hash ring for each physical server.
   - Example: Each server can have multiple virtual nodes spread across the ring.

   - **Advantages of Virtual Nodes:**
     - **Improved Load Balancing:** Helps in distributing data more evenly.
     - **Flexibility:** Makes it easier to adjust the load distribution by changing the number of virtual nodes per server.

4. **Applications of Consistent Hashing:**

   - **Distributed Databases:** Used in systems like Cassandra and DynamoDB to distribute data across nodes.
   - **Caching Systems:** Used in caching solutions like Memcached and Redis to distribute cached data.
   - **Load Balancing:** Helps in distributing requests evenly across multiple servers in load balancing solutions.

## Summary

Consistent hashing is a method to distribute data evenly across servers, handling changes smoothly with minimal disruption. It uses a circular hash space and assigns data to the nearest server in the clockwise direction. Virtual nodes improve load balancing and flexibility. Applications include distributed databases, caching systems, and load balancing, with advantages like scalability and fault tolerance, but also some complexity in implementation.

|                       | **Simple Hashing**                                                            | **Consistent Hashing**                                                                          |
| --------------------- | ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| **Method**            | Uses a hash function to map data to a fixed number of buckets (servers).      | Uses a hash function to map data and servers to positions on a circular hash space (hash ring). |
| **Data Distribution** | Even distribution only if the number of buckets is fixed and data is uniform. | Even distribution across servers; minimal data reassignment when servers change.                |
| **Server Changes**    | Adding/removing a server requires rehashing almost all data.                  | Only a small portion of data needs reassignment when servers change.                            |
| **Advantages**        | Simple and easy to implement; works well with a fixed number of servers.      | Highly scalable and fault-tolerant; minimal data movement with server changes.                  |
| **Disadvantages**     | Inflexible and not suitable for frequently changing server numbers.           | More complex to implement; may require virtual nodes for even load distribution.                |
