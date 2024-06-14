# 7. RocksDB

RocksDB is a high-performance embedded database for key-value data, optimized for fast storage environments. It is designed to leverage the strengths of modern storage hardware to provide low-latency, high-throughput database operations.

### Key Concepts:

1. **Memtable:**
2. **Write-Ahead Log:**
3. **Sorted Strings Table (SSTable):**

## Memtable

A memtable is an in-memory data structure where all new writes are first recorded. It is a key-value store that keeps the most recent updates before they are flushed to disk.

**Characteristics:**

- **Fast Writes:** Allows for quick write operations as data is kept in memory.
- **Temporary Storage:** Holds data until it is written to a more permanent on-disk structure like an SSTable.

**Process:**

1. New data is written to the memtable.
2. Once the memtable reaches a certain size, it is flushed to disk, creating a new SSTable.
3. During this flush, the data is also written to the write-ahead log to ensure durability.

## Write-Ahead Log (WAL)

The write-ahead log (WAL) is a persistent log file where all write operations are recorded before they are applied to the memtable. This ensures data durability and consistency.

**Characteristics:**

- **Durability:** Ensures that no data is lost in case of a crash, as all operations can be replayed from the WAL.
- **Sequential Writes:** WAL writes are sequential, which is efficient for modern storage devices.

**Process:**

1. Every write operation is logged in the WAL before being added to the memtable.
2. If the system crashes, the database can recover by replaying the WAL to reconstruct the memtable.

## Sorted Strings Table (SSTable)

An SSTable is an immutable, sorted, and indexed file on disk that stores data in key-value format. It is created by flushing the memtable to disk.

**Characteristics:**

- **Immutable:** Once written, SSTables are never modified.
- **Sorted:** Keys are stored in sorted order, facilitating efficient range queries.
- **Indexed:** Each SSTable has an index to quickly locate keys.

**Process:**

1. When the memtable is full, it is flushed to disk, creating a new SSTable.
2. SSTables are periodically merged and compacted to optimize read performance and reclaim space.

### Example in Rust

Using the `rust-rocksdb` crate to demonstrate the basic operations:

First, add the `rust-rocksdb` dependency to your `Cargo.toml` file:

```toml
[dependencies]
rocksdb = "0.15.0"
```

Then, use the following code to interact with RocksDB:

```rust
use rocksdb::{Options, DB};

fn main() {
    // Create a new RocksDB database
    let path = "path/to/rocksdb";
    let db = DB::open_default(path).unwrap();

    // Put some data into the database
    db.put(b"key1", b"value1").unwrap();
    db.put(b"key2", b"value2").unwrap();

    // Get data from the database
    match db.get(b"key1") {
        Ok(Some(value)) => println!("Retrieved value: {:?}", String::from_utf8(value).unwrap()),
        Ok(None) => println!("Value not found"),
        Err(e) => println!("Error reading value: {:?}", e),
    }

    // Delete a key-value pair
    db.delete(b"key2").unwrap();

    // Close the database
    drop(db);
}
```

## Summary

RocksDB is a high-performance embedded database designed for modern storage hardware. It uses memtables for fast in-memory writes, write-ahead logs (WAL) for durability and crash recovery, and SSTables for efficient, sorted, and indexed on-disk storage. These components work together to provide a robust, high-throughput database solution.
