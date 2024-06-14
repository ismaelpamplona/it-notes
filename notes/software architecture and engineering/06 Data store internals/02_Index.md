# 2. Index

Imagine you have a big book with thousands of pages. If you want to find a specific topic, you don't flip through every page. Instead, you use the index at the back of the book, which tells you exactly where to find what you're looking for. In computing, an index works the same way: it helps you find data quickly without searching through everything.

An index is a data structure that improves the speed of data retrieval operations. It works like a map, pointing to the location of the data without needing to scan the entire dataset.

### How to Implement an Efficient Index for a Messaging System

In a messaging system, users send and receive many messages. An efficient index helps quickly find specific messages based on various criteria like sender, recipient, timestamp, or keywords.

1. **Choose the Right Data Structure:**

   - **B-tree:** A balanced tree structure that maintains sorted data and allows for fast lookup, insertion, and deletion.
   - **Hash Table:** Uses a hash function to compute an index into an array of buckets, from which the desired value can be found.

2. **Define Indexing Criteria:**

   - **Primary Index:** Usually on a unique identifier like message ID.
   - **Secondary Index:** On frequently queried fields like sender, recipient, or timestamp.

3. **Implementing the Index:**

   - **Primary Index:**

     - Use a B-tree or hash table for the message ID.
     - Ensures quick access to messages by their unique identifier.

   - **Secondary Index:**
     - Create additional indexes on fields like sender, recipient, and timestamp.
     - For example, a B-tree index on timestamps for quick retrieval of recent messages.

### Example in SQL:

Creating indexes for a messaging table in SQL:

```sql
CREATE TABLE messages (
    message_id SERIAL PRIMARY KEY,
    sender_id INT,
    recipient_id INT,
    timestamp TIMESTAMP,
    message_text TEXT
);

-- Primary index on message_id (automatically created as PRIMARY KEY)
-- Secondary index on sender_id
CREATE INDEX idx_sender_id ON messages(sender_id);

-- Secondary index on recipient_id
CREATE INDEX idx_recipient_id ON messages(recipient_id);

-- Secondary index on timestamp
CREATE INDEX idx_timestamp ON messages(timestamp);
```

### Example in Rust:

Using a Rust example with a hypothetical in-memory storage for indexing messages:

**BTreeMap**:

```rust
use std::collections::{BTreeMap, HashSet};

struct Message {
    message_id: u32,
    sender_id: u32,
    recipient_id: u32,
    timestamp: u64,
    message_text: String,
}

struct MessageSystem {
    messages: BTreeMap<u32, Message>,
    sender_index: BTreeMap<u32, HashSet<u32>>, // sender_id to message_ids
    recipient_index: BTreeMap<u32, HashSet<u32>>, // recipient_id to message_ids
    timestamp_index: BTreeMap<u64, HashSet<u32>>, // timestamp to message_ids
}

impl MessageSystem {
    fn new() -> Self {
        MessageSystem {
            messages: BTreeMap::new(),
            sender_index: BTreeMap::new(),
            recipient_index: BTreeMap::new(),
            timestamp_index: BTreeMap::new(),
        }
    }

    fn add_message(&mut self, message: Message) {
        self.sender_index.entry(message.sender_id)
            .or_insert(HashSet::new()).insert(message.message_id);
        self.recipient_index.entry(message.recipient_id)
            .or_insert(HashSet::new()).insert(message.message_id);
        self.timestamp_index.entry(message.timestamp)
            .or_insert(HashSet::new()).insert(message.message_id);
        self.messages.insert(message.message_id, message);
    }

    fn get_messages_by_sender(&self, sender_id: u32) -> Vec<&Message> {
        if let Some(message_ids) = self.sender_index.get(&sender_id) {
            message_ids.iter()
                .filter_map(|id| self.messages.get(id))
                .collect()
        } else {
            Vec::new()
        }
    }

}
```

**HashMap**:

```rust
use std::collections::{HashMap, HashSet};

struct Message {
    message_id: u32,
    sender_id: u32,
    recipient_id: u32,
    timestamp: u64,
    message_text: String,
}

struct MessageSystem {
    messages: HashMap<u32, Message>,
    sender_index: HashMap<u32, HashSet<u32>>, // sender_id to message_ids
    recipient_index: HashMap<u32, HashSet<u32>>, // recipient_id to message_ids
    timestamp_index: HashMap<u64, HashSet<u32>>, // timestamp to message_ids
}

impl MessageSystem {
    fn new() -> Self {
        MessageSystem {
            messages: HashMap::new(),
            sender_index: HashMap::new(),
            recipient_index: HashMap::new(),
            timestamp_index: HashMap::new(),
        }
    }

    fn add_message(&mut self, message: Message) {
        self.sender_index.entry(message.sender_id)
            .or_insert(HashSet::new()).insert(message.message_id);
        self.recipient_index.entry(message.recipient_id)
            .or_insert(HashSet::new()).insert(message.message_id);
        self.timestamp_index.entry(message.timestamp)
            .or_insert(HashSet::new()).insert(message.message_id);
        self.messages.insert(message.message_id, message);
    }

    fn get_messages_by_sender(&self, sender_id: u32) -> Vec<&Message> {
        if let Some(message_ids) = self.sender_index.get(&sender_id) {
            message_ids.iter()
                .filter_map(|id| self.messages.get(id))
                .collect()
        } else {
            Vec::new()
        }
    }

    // Similar methods can be implemented for recipient and timestamp indices
}
```

# Apache Kafka and Indexing

Apache Kafka is a distributed streaming platform used for building real-time data pipelines and streaming applications. It is designed to handle high throughput and provide durable, fault-tolerant messaging. One of the key components that contribute to Kafka's performance is its efficient use of indexing.

## Indexing in Kafka

Kafka uses a unique approach to indexing messages to ensure fast and efficient retrieval.

### Key Components:

1. **Id Range Index:**

   - This is an index that maps ranges of message IDs to specific segments. Each range corresponds to a segment where the messages are stored.
   - Example:
     - ID Range 0-3 maps to `segment-0`.
     - ID Range 4-7 maps to `segment-1`.
     - ID Range 8-11 maps to `segment-2`.

2. **Segments:**

   - A segment is a portion of the log where messages are stored sequentially. Kafka breaks down logs into smaller, more manageable segments.
   - Each segment contains a series of messages and has its own index file.

3. **Segment Index:**
   - Each segment has an index file that maps message IDs to their position within the segment.
   - This allows Kafka to quickly locate a message by its ID within a specific segment.

### How it Works:

1. **Message Retrieval:**

   - To retrieve a message with a specific ID (e.g., ID = 2), Kafka first uses the id range index to identify the segment containing the message. For ID = 2, it points to `segment-0`.
   - Next, Kafka retrieves the message bytes from `segment-0`.
   - Finally, Kafka looks up the message position in the segment-0 index, which gives the exact byte offset within the segment where the message is stored.

2. **Binary Search:**
   - The id range index supports binary search, allowing for efficient lookup of the segment containing the desired message.
   - Once the segment is identified, the segment index provides a direct mapping to the message's position, ensuring fast access.

### Benefits:

- **Efficiency:** Segment-based indexing reduces the need to scan through large log files, significantly speeding up message retrieval.
- **Scalability:** By dividing logs into segments and indexing them, Kafka can handle large volumes of messages efficiently.
- **Durability:** Each segment is a separate file, which can be replicated and stored across multiple nodes for fault tolerance.

## Summary

An index is like a map that helps you find data quickly without scanning everything. In a messaging system, implementing an efficient index involves choosing the right data structure (like B-tree or hash table), defining primary and secondary indexes, and using them to speed up data retrieval. Proper indexing improves the performance and scalability of the system.

Apache Kafka's use of segment-based indexing allows for efficient message retrieval by mapping ranges of message IDs to specific segments and maintaining segment-specific indexes. This approach ensures fast access to messages, improves scalability, and enhances fault tolerance, making Kafka a robust solution for real-time data streaming and processing.

# 3. Time series data

- How to store and retrieve time series data at scale and with low latency.
