# 5. Data Encoding Formats

Imagine you want to send a secret message to your friend. Data encoding formats are like different ways to write or encode that message so your friend can understand it. There are different formats depending on how you want to send the message.

### Textual Formats:

- **Textual formats** are like writing a message with letters and words that you can read.
- Examples: JSON, XML
- Easy to read and understand, but can be larger and slower to process.

### Binary Formats:

- **Binary formats** are like writing a message with special codes or symbols that a computer can understand.
- Examples: Protocol Buffers, Avro
- Harder for humans to read, but smaller and faster for computers to process.

## Deep Dive and Important Points:

### Textual vs Binary Formats:

1. **Textual Formats:**

   - **Definition:** Data is encoded as readable text.
   - **Examples:** JSON, XML
   - **Characteristics:**

     - **Human-readable:** Easy to read and understand.
     - **Larger size:** Takes up more space.
     - **Slower processing:** Takes longer for computers to process.

   - **Example:**
     - JSON: `{ "name": "Alice", "age": 12 }`
     - XML: `<person><name>Alice</name><age>12</age></person>`

2. **Binary Formats:**

   - **Definition:** Data is encoded in a binary format, which is not readable by humans.
   - **Examples:** Protocol Buffers, Avro
   - **Characteristics:**

     - **Not human-readable:** Hard to read and understand.
     - **Smaller size:** Takes up less space.
     - **Faster processing:** Quick for computers to process.

   - **Example:**
     - Protocol Buffers: Binary encoded data that needs special tools to read.

### Schema Sharing Options:

1. **Definition:** A schema defines the structure of the data, like a template or blueprint.

2. **Options:**

   - **Embedded Schema:**

     - The schema is included within the data itself.
     - Makes it easy to understand the data structure, but increases data size.

   - **External Schema:**

     - The schema is stored separately from the data.
     - Keeps data size small, but requires a way to access the schema.

   - **Example:**
     - Embedded: JSON data with schema: `{ "type": "object", "properties": { "name": { "type": "string" } }, "name": "Alice" }`
     - External: JSON data: `{ "name": "Alice" }` with separate schema file.

### Backward Compatibility and Forward Compatibility:

1. **Backward Compatibility:**

   - **Definition:** Newer versions of the data format can be read by older systems.
   - **Importance:** Ensures old systems can still understand new data.

2. **Forward Compatibility:**

   - **Definition:** Older versions of the data format can be read by newer systems.
   - **Importance:** Ensures new systems can understand old data.

   - **Example:**
     - Adding new fields in JSON: Older systems ignore new fields they don't understand.
     - Removing fields in Protocol Buffers: New systems handle missing fields gracefully.

## Summary

**Textual formats** are easy for humans to read but take up more space and are slower for computers. **Binary formats** are smaller and faster for computers but harder for humans to read. **Schema sharing** can be done by embedding the schema within the data or keeping it separate. **Backward compatibility** ensures old systems can read new data, while **forward compatibility** ensures new systems can read old data. These concepts help in efficiently storing and processing data while maintaining compatibility across different systems.
