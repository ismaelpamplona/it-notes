# 3. Time Series Data

Time series data consists of sequences of data points collected or recorded at successive points in time. Examples include stock prices, temperature readings, and server performance metrics.

Imagine you have a diary where you write down the temperature every hour. Each entry has a timestamp (the time you wrote it) and the temperature. This is similar to time series data, where each data point has a timestamp.

### How to Store and Retrieve Time Series Data at Scale and with Low Latency

Storing and retrieving time series data efficiently requires specialized databases and techniques designed to handle the unique characteristics of time series data.

### Storing Time Series Data

1. **Time Series Databases (TSDBs):**

   - **Examples:** InfluxDB, TimescaleDB, OpenTSDB.
   - **Features:**
     - Optimized for high write and query throughput.
     - Efficient data compression to handle large volumes of data.
     - Built-in support for time-based queries and aggregations.

2. **Data Partitioning:**

   - **Horizontal Partitioning (Sharding):** Dividing the data into smaller, more manageable pieces, each stored on different database servers.
   - **Time-Based Partitioning:** Organizing data by time intervals (e.g., hourly, daily) to improve query performance and data management.

3. **Compression:**
   - **Lossless Compression:** Reduces storage space without losing any data, ensuring data integrity.
   - **Time-Based Compression Algorithms:** Specifically designed for time series data to store more data efficiently.

### Retrieving Time Series Data

1. **Indexing:**

   - **Time-Based Indexing:** Indexing data based on timestamps to speed up time-range queries.
   - **Secondary Indexes:** Additional indexes on fields other than time (e.g., sensor ID) to improve query performance.

2. **Query Optimization:**

   - **Downsampling:** Reducing the resolution of data by aggregating data points over time intervals (e.g., average temperature per hour).
   - **Pre-Aggregation:** Storing pre-computed aggregates to speed up query responses.

3. **Caching:**
   - **In-Memory Caching:** Storing frequently accessed data in memory to reduce latency.
   - **Time-Window Caching:** Keeping the most recent data in memory, as recent data is often accessed more frequently.

### Example in SQL (TimescaleDB)

**Creating a Time Series Table:**

```sql
CREATE TABLE temperature_readings (
    time TIMESTAMPTZ NOT NULL,
    sensor_id INT,
    temperature DOUBLE PRECISION,
    PRIMARY KEY (time, sensor_id)
);

SELECT create_hypertable('temperature_readings', 'time');
```

**Inserting Data:**

```sql
INSERT INTO temperature_readings (time, sensor_id, temperature)
VALUES (NOW(), 1, 22.5);
```

**Querying Data:**

```sql
-- Retrieve data for the last 24 hours
SELECT time, temperature
FROM temperature_readings
WHERE time > NOW() - INTERVAL '24 hours';

-- Downsample data to hourly averages
SELECT time_bucket('1 hour', time) AS hour, AVG(temperature) AS avg_temp
FROM temperature_readings
GROUP BY hour;
```

### Example in Rust (InfluxDB)

**Inserting Data:**

```rust
use influxdb::{Client, Query, Timestamp, WriteQuery};

#[tokio::main]
async fn main() {
    let client = Client::new("http://localhost:8086", "mydb");

    let query = WriteQuery::new(Timestamp::Now, "temperature_readings")
        .add_field("temperature", 22.5)
        .add_tag("sensor_id", "1");

    client.query(&query).await.unwrap();
}
```

**Querying Data:**

```rust
use influxdb::{Client, Query};

#[tokio::main]
async fn main() {
    let client = Client::new("http://localhost:8086", "mydb");

    let query = Query::raw_read_query("SELECT * FROM temperature_readings WHERE time > now() - 24h");

    let results = client.query(&query).await.unwrap();
    println!("{:?}", results);
}
```

## IoT Examples

### Temperature Readings

**Scenario:** An IoT network of sensors records temperature readings every minute across a city.

**Storage Strategy:**

- Use a TSDB like InfluxDB to store temperature readings.
- Partition data by sensor location and time intervals (e.g., daily partitions).
- Compress data to save storage space.

**Retrieval Strategy:**

- Index data by sensor ID and timestamp for fast lookups.
- Use caching for frequently accessed recent data.
- Optimize queries to fetch data for specific sensors and time ranges.

### Stock Trading

**Scenario:** A stock trading platform records the price of stocks every second.

**Storage Strategy:**

- Use a high-performance distributed database like Apache Cassandra.
- Partition data by stock ticker symbol and time intervals (e.g., hourly partitions).
- Use efficient write operations to handle high-frequency data ingestion.

**Retrieval Strategy:**

- Index data by stock ticker and timestamp.
- Use in-memory caching for recent trading data.
- Optimize queries to fetch price data for specific stocks and time ranges.

### Social Media

**Scenario:** A social media platform records user activity (e.g., posts, likes) with timestamps.

**Storage Strategy:**

- Use a TSDB like TimescaleDB.
- Partition data by user ID and time intervals (e.g., daily partitions).
- Compress data to save space and improve performance.

**Retrieval Strategy:**

- Index data by user ID and timestamp.
- Cache recent activity data for quick access.
- Optimize queries to fetch activity data for specific users and time ranges.

## Summary

Storing and retrieving time series data at scale and with low latency requires using specialized time series databases, efficient data partitioning, and compression techniques. By leveraging time-based indexing, query optimization, and caching strategies, you can ensure high performance and low latency for time series data applications.

In IoT applications, stock trading, social media, and temperature readings, these strategies ensure that large volumes of time series data can be managed and accessed quickly and efficiently.
