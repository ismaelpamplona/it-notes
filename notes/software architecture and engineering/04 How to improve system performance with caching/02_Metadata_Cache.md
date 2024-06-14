# 2. Metadata Cache

Imagine you have a special notebook where you keep notes about your favorite books, like their titles, authors, and a short summary. A metadata cache is like that notebook, helping you quickly remember important details without having to look up each book again.

### Cache-aside Pattern:

- **Cache-aside Pattern:** This is like checking your notebook first for the information. If the information isn't there, you look up the book and then write the details in your notebook for next time.

### Read-through and Write-through Patterns:

- **Read-through Pattern:** This is like having an assistant who checks the notebook for you when you need information. If it's not in the notebook, they find the book, add the details to the notebook, and give you the information.
- **Write-through Pattern:** This is like having an assistant who writes the book details in the notebook at the same time you get a new book. This way, the notebook is always up to date.

### Write-behind (Write-back) Pattern:

- **Write-behind Pattern:** This is like having an assistant who quickly notes down new book details in a temporary list and updates your notebook later when there's more time.

## Deep Dive and Important Points:

### Cache-aside Pattern:

1. **Definition:**

   - The application is responsible for loading data into the cache.
   - Data is loaded into the cache only when it is needed (lazy loading).

2. **How it Works:**

   - **Check Cache:** Look in the cache for the data.
   - **Load Data:** If the data is not in the cache, load it from the primary data store.
   - **Update Cache:** Store the loaded data in the cache for future use.

   ```mermaid
   sequenceDiagram
       participant Application
       participant Cache
       participant Database

       Application->>Cache: Check for Data
       Cache-->>Application: Data Not Found
       Application->>Database: Load Data
       Database-->>Application: Data Loaded
       Application->>Cache: Update Cache
       Cache-->>Application: Cache Updated
   ```

   - The **Application** checks the **Cache** for data.
   - If not found, it loads the data from the **Database** and updates the **Cache**.

3. **Pros**:

   - Widely used pattern

4. **Cons**:

   - Les suitable for latency-critical systems (every cache miss results in three round trips)
   - Stale data when data changes frequently in the data store (mitigated by setting expiration time on cache entries)
   - Prone to cache stampede behavior (multiple threads simultaneously query the same entry from the data store)

### Read-through and Write-through Patterns:

1. **Read-through Pattern:**

   - **Definition:** The cache is responsible for loading data from the database.
   - **How it Works:**
     - The application requests data from the cache.
     - If the data is not in the cache, the cache itself loads the data from the database.

   ```mermaid
   sequenceDiagram
       participant Application
       participant Cache
       participant Database

       Application->>Cache: Request Data
       Cache-->>Application: Data Not Found
       Cache->>Database: Load Data
       Database-->>Cache: Data Loaded
       Cache-->>Application: Data from Cache
   ```

   - The **Application** requests data from the **Cache**.
   - If not found, the **Cache** loads data from the **Database** and returns it to the **Application**.

2. **Write-through Pattern:**

   - **Definition:** Data is written to the cache and the primary data store simultaneously.
   - **How it Works:**
     - When the application updates data, the cache updates the primary data store.

   ```mermaid
   sequenceDiagram
       participant Application
       participant Cache
       participant Database

       Application->>Cache: Update Data
       Cache->>Database: Write Data
       Database-->>Cache: Data Written
       Cache-->>Application: Cache Updated
   ```

   - The **Application** updates data in the **Cache**.
   - The **Cache** writes the data to the **Database** and confirms the update.

3. **Pros**:

   - (both patterns) Simplify data access code on the application side.
   - (read-through) Helps to mitigate the cache stampede problem.
   - Request coalescing technique can reduce the load on the data store by combining multiple requests for the same data.

4. **Cons**:

   - Cache may contain a lot of rarely used data. (a problem for small caches)
   - Cache becomes a critical component for the system.

### Write-behind (Write-back) Pattern:

1. **Definition:**

   - Data is initially written to the cache, and the cache updates the primary data store later.
   - This allows for faster write operations.

2. **How it Works:**

   - **Write to Cache:** The application writes data to the cache.
   - **Deferred Write:** The cache schedules the update to the primary data store for later.

   ```mermaid
   sequenceDiagram
       participant Application
       participant Cache
       participant Database

       Application->>Cache: Write Data
       Cache-->>Application: Cache Updated
       Note over Cache,Database: Scheduled Write to Database
       Cache->>Database: Write Data
       Database-->>Cache: Data Written
   ```

   - The **Application** writes data to the **Cache**.
   - The **Cache** updates the **Database** at a later time.

3. **Pros**:

   - Better write performance (higher throughput, lower latency)

4. **Cons**:

   - Data can be lost (mitigated by data replication in cache)

## Summary

A metadata cache helps store and quickly access important details. The **cache-aside pattern** involves the application checking the cache first and updating it as needed. The **read-through pattern** has the cache load data from the database automatically, while the **write-through pattern** ensures data is updated in both the cache and database simultaneously. The **write-behind pattern** allows data to be written to the cache first and then the database later, improving write performance.
