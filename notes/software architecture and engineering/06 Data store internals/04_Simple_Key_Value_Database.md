# 4. Simple Key-Value Database

A key-value database is a type of NoSQL database that stores data as a collection of key-value pairs. Each key is unique and is used to retrieve the corresponding value, much like a dictionary in programming.

## How to Build a Simple Key-Value Database

### Key Concepts:

1. **Data Structure:**

   - Use a `HashMap` to store key-value pairs in memory.
   - Persist data to disk using log files to ensure durability.

2. **Operations:**

   - **Put:** Add or update a key-value pair.
   - **Get:** Retrieve the value for a given key.
   - **Delete:** Remove a key-value pair.

3. **Persistence:**
   - Append changes to a log file on disk.
   - Periodically snapshot the in-memory `HashMap` to disk for faster recovery.

### Basic Implementation in Rust:

```rust
use std::collections::HashMap;
use std::fs::{File, OpenOptions};
use std::io::{self, BufRead, BufReader, Write};

struct KeyValueStore {
    map: HashMap<String, String>,
    log: File,
}

impl KeyValueStore {
    fn new(log_path: &str) -> io::Result<Self> {
        let log = OpenOptions::new().append(true).create(true).open(log_path)?;
        let map = HashMap::new();
        Ok(KeyValueStore { map, log })
    }

    fn put(&mut self, key: String, value: String) -> io::Result<()> {
        self.map.insert(key.clone(), value.clone());
        writeln!(self.log, "PUT {} {}", key, value)?;
        self.log.flush()
    }

    fn get(&self, key: &str) -> Option<&String> {
        self.map.get(key)
    }

    fn delete(&mut self, key: &str) -> io::Result<()> {
        self.map.remove(key);
        writeln!(self.log, "DEL {}", key)?;
        self.log.flush()
    }

    fn load(log_path: &str) -> io::Result<Self> {
        let file = File::open(log_path)?;
        let reader = BufReader::new(file);
        let mut map = HashMap::new();

        for line in reader.lines() {
            let line = line?;
            let parts: Vec<&str> = line.splitn(3, ' ').collect();
            match parts.as_slice() {
                ["PUT", key, value] => { map.insert(key.to_string(), value.to_string()); },
                ["DEL", key] => { map.remove(*key); },
                _ => (),
            }
        }

        let log = OpenOptions::new().append(true).open(log_path)?;
        Ok(KeyValueStore { map, log })
    }
}

fn main() -> io::Result<()> {
    let mut kv_store = KeyValueStore::new("kv.log")?;
    kv_store.put("key1".to_string(), "value1".to_string())?;
    kv_store.put("key2".to_string(), "value2".to_string())?;
    println!("{:?}", kv_store.get("key1")); // Some("value1")
    kv_store.delete("key1")?;
    println!("{:?}", kv_store.get("key1")); // None
    Ok(())
}
```

## Log Compaction

### What is Log Compaction?

Log compaction is a process used to reclaim storage space and improve performance in a log-structured storage system. It involves consolidating and removing redundant or obsolete entries from the log file.

### How it Works:

1. **Identify Obsolete Entries:**

   - Scan the log file to identify entries that have been superseded by more recent updates or deletions.

2. **Rewrite Log:**
   - Create a new log file that only includes the most recent entries for each key.
   - Discard outdated entries to free up disk space.

### Example:

Consider the following log entries:

```
PUT key1 value1
PUT key2 value2
PUT key1 value3
DEL key2
```

After log compaction, the log would contain:

```
PUT key1 value3
```

The entries `PUT key1 value1` and `PUT key2 value2` are obsolete because they have been updated or deleted.

### Implementation:

To implement log compaction, you can periodically perform the following steps:

1. **Scan the Log:**

   - Read the current log file and build a new in-memory `HashMap` with the latest entries.

2. **Write a New Log:**

   - Write the current state of the `HashMap` to a new log file.

3. **Replace the Old Log:**
   - Atomically replace the old log file with the new compacted log file.

## Summary

Building a simple key-value database involves using a `HashMap` for in-memory storage and log files for persistence. Key operations include adding, retrieving, and deleting key-value pairs. Log compaction helps maintain performance and reclaim storage space by removing obsolete entries from the log file.
