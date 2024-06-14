# 1. Deduplication Cache

Imagine you have a box where you store your favorite toy cars. A deduplication cache is like that box, but it only keeps one of each kind of toy car, so you don't have duplicates.

## Simple Explanation:

### Local vs External Cache:

- **Local Cache:** This is like keeping your toy cars in a small box in your room.
- **External Cache:** This is like keeping your toy cars in a big storage room outside your house.

### Adding Data to Cache:

- **Explicitly:** This is like you putting a toy car in the box yourself.
- **Implicitly:** This is like the box automatically getting a toy car when you play with it.

### Cache Data Eviction:

- **Size-based:** This is like removing old toy cars when your box gets too full.
- **Time-based:** This is like removing toy cars that you haven't played with for a long time.
- **Explicit:** This is like deciding which toy cars to remove from the box yourself.

### Expiration vs Refresh:

- **Expiration:** This is like setting a rule that a toy car will be removed if you don't play with it for a week.
- **Refresh:** This is like updating the time you last played with a toy car every time you play with it, so it stays in the box longer.

## Deep Dive and Important Points:

### Local vs External Cache:

1. **Local Cache:**

   - **Definition:** A cache stored locally on the same system or device.
   - **Characteristics:**
     - **Fast Access:** Quick access to data because it's stored nearby.
     - **Limited Size:** Limited by the storage capacity of the local device.
     - **Use Cases:** Web browser cache, application cache.

2. **External Cache:**

   - **Definition:** A cache stored externally, often on a remote server or dedicated caching system.
   - **Characteristics:**
     - **Larger Capacity:** Can handle more data because it's stored on a server.
     - **Slower Access:** Slightly slower access due to network latency.
     - **Use Cases:** CDN cache, database cache.

### Adding Data to Cache:

1. **Explicitly:**

   - **Definition:** Manually adding data to the cache.
   - **How it Works:**
     - You decide which data to add to the cache.

   ```mermaid
   sequenceDiagram
       participant User
       participant Cache

       User->>Cache: Add Data
       Cache-->>User: Data Added
   ```

   - The **User** adds data to the **Cache** manually.

2. **Implicitly:**

   - **Definition:** Automatically adding data to the cache based on usage.
   - **How it Works:**
     - The system decides which data to add based on access patterns.

   ```mermaid
   sequenceDiagram
       participant System
       participant Cache

       System->>Cache: Access Data
       Cache-->>System: Data Added Automatically
   ```

   - The **System** automatically adds data to the **Cache** when accessed.

### Cache Data Eviction:

1. **Size-based Eviction:**

   - **Definition:** Removing data when the cache reaches a certain size.
   - **How it Works:**
     - Oldest or least used data is removed to make space.

   ```mermaid
   sequenceDiagram
       participant Cache
       participant Data

       Cache->>Data: Evict Old Data
       Note over Cache: Size Limit Reached
   ```

   - The **Cache** evicts old data when it reaches its size limit.

2. **Time-based Eviction:**

   - **Definition:** Removing data that hasn't been used for a certain period.
   - **How it Works:**
     - Data is removed if it hasn't been accessed within a specified time.

   ```mermaid
   sequenceDiagram
       participant Cache
       participant Data

       Cache->>Data: Evict Stale Data
       Note over Cache: Time Limit Reached
   ```

   - The **Cache** evicts data that hasn't been used within the time limit.

3. **Explicit Eviction:**

   - **Definition:** Manually removing data from the cache.
   - **How it Works:**
     - The user or system explicitly decides which data to remove.

   ```mermaid
   sequenceDiagram
       participant User
       participant Cache

       User->>Cache: Remove Data
       Cache-->>User: Data Removed
   ```

   - The **User** removes specific data from the **Cache**.

### Expiration vs Refresh:

1. **Expiration:**

   - **Definition:** Data is automatically removed from the cache after a set period.
   - **How it Works:**
     - Data is tagged with an expiration time and removed when that time is reached.

   ```mermaid
   sequenceDiagram
       participant Cache
       participant Data

       Cache->>Data: Set Expiration Time
       Cache->>Data: Remove After Expiration
   ```

   - The **Cache** sets an expiration time and removes data when it expires.

2. **Refresh:**

   - **Definition:** Updating the access time of data each time it is used to extend its validity.
   - **How it Works:**
     - The access time is reset each time the data is accessed.

   ```mermaid
   sequenceDiagram
       participant Cache
       participant Data

       Cache->>Data: Update Access Time
       Note over Cache: Data Accessed
   ```

   - The **Cache** updates the access time of data each time it is used.

## Summary

A deduplication cache ensures that only unique data is stored. **Local caches** are fast but limited in size, while **external caches** have more capacity but slower access. Data can be added to caches **explicitly** (manually) or **implicitly** (automatically). Data eviction can be **size-based** (remove old data when full), **time-based** (remove data not used for a while), or **explicit** (manual removal). **Expiration** removes data after a set time, while **refresh** extends the life of data with each use.
