# 5. Rebalancing Partitions

Imagine you have a classroom with many students, and you want to make sure each group has the same number of students. If some groups have too many students while others have too few, you move students around to balance the groups. In software, rebalancing partitions means adjusting the distribution of data or tasks across different servers to ensure an even load.

Rebalancing partitions is like making sure everyone has an equal amount of work. For example:

- If one server has too much data, some data is moved to another server with less data.
- This helps in keeping things fair and efficient.

1. **Why Rebalance Partitions?**

   - **Uneven Data Distribution:** When some partitions have much more data than others.
   - **Hot Keys:** When certain data is accessed more frequently, causing uneven load.
   - **Server Failures:** When a server fails, its data needs to be redistributed to other servers.

2. **How to Rebalance Partitions:**

   - **Splitting a Shard:**

     - When a shard (partition) grows too big, it can be split into smaller shards.
     - Example: A 128 MB shard can be split into two 64 MB shards.
     - This is mainly a metadata change, but it might involve moving data if new servers are added.

   - **Shard Migration:**

     - A process that moves data from one server to another to balance the load.
     - Triggered by adding or removing servers in the cluster.
     - Managed by a background process called the balancer.

   - **Merging Shards:** When a shard becomes too small, it can be merged with an adjacent shard to optimize storage.

3. **Rebalancing Strategies:**

   - **Option 1: Split a Shard When It Grows Too Big**

     - This involves splitting a large shard into smaller ones.
     - Used in systems like MongoDB and HBase.

   - **Option 2: Split Shards When Adding a New Server**

     - When a new server is added, existing shards are split, and some are moved to the new server.
     - Used in systems like Cassandra.

   - **Option 3: Fixed Number of Shards**
     - The system maintains a fixed number of shards regardless of the data size.
     - Easier to manage but requires careful planning of the initial number of shards.
     - Used in systems like Couchbase and Elasticsearch.

## Summary

Rebalancing partitions ensures an even distribution of data and tasks across servers to maintain efficiency and performance. Techniques include splitting large shards, migrating shards when servers are added or removed, and maintaining a fixed number of shards. Each strategy has its advantages and challenges, and the choice depends on the specific requirements of the system.

| **Rebalancing Strategy**                              | **Partitioning Strategy** | **Real-world Examples**  |
| ----------------------------------------------------- | ------------------------- | ------------------------ |
| split a shard when it grows beyond the specified size | range, hash               | MongoDB, HBase           |
| split shards when adding a new server                 | hash                      | Cassandra                |
| fixed number of shards                                | hash, lookup              | Couchbase, Elasticsearch |
