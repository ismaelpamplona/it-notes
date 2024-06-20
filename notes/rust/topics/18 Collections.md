
# Collections in Rust

## Overview

Collections in Rust are data structures that allow you to store and manage multiple values efficiently. Rust provides several built-in collections, each with different use cases and performance characteristics. The most common collections in Rust are `Vec`, `HashMap`, and `HashSet`.

## Vector (`Vec`)

A `Vec` (short for vector) is a growable array type in Rust. It allows you to store a dynamic number of elements and provides various methods for adding, removing, and accessing elements.

### Example

```rust
fn main() {
    let mut v = Vec::new();

    v.push(1);
    v.push(2);
    v.push(3);

    println!("Vector: {:?}", v);

    let third = v[2];
    println!("The third element is {}", third);

    match v.get(2) {
        Some(third) => println!("The third element is {}", third),
        None => println!("There is no third element."),
    }

    for i in &v {
        println!("{}", i);
    }

    for i in &mut v {
        *i += 50;
    }

    println!("Updated Vector: {:?}", v);
}
```

### Key Methods

- `push`: Adds an element to the end of the vector.
- `pop`: Removes the last element from the vector.
- `get`: Returns a reference to an element by index.
- `remove`: Removes an element by index and returns it.

## HashMap

A `HashMap` is a collection that stores key-value pairs. It allows for efficient retrieval of values based on their keys.

### Example

```rust
use std::collections::HashMap;

fn main() {
    let mut scores = HashMap::new();

    scores.insert(String::from("Blue"), 10);
    scores.insert(String::from("Yellow"), 50);

    let team_name = String::from("Blue");
    let score = scores.get(&team_name);

    match score {
        Some(score) => println!("The score for {} is {}", team_name, score),
        None => println!("No score found for {}", team_name),
    }

    for (key, value) in &scores {
        println!("{}: {}", key, value);
    }
}
```

### Key Methods

- `insert`: Adds a key-value pair to the map.
- `get`: Retrieves a reference to the value associated with a key.
- `remove`: Removes a key-value pair from the map by key.
- `contains_key`: Checks if a key is present in the map.

## HashSet

A `HashSet` is a collection of unique values. It provides efficient methods for checking membership, adding, and removing elements.

### Example

```rust
use std::collections::HashSet;

fn main() {
    let mut books = HashSet::new();

    books.insert("The Great Gatsby");
    books.insert("To Kill a Mockingbird");
    books.insert("1984");

    if books.contains("1984") {
        println!("The set contains 1984.");
    }

    books.remove("1984");

    if !books.contains("1984") {
        println!("The set no longer contains 1984.");
    }

    for book in &books {
        println!("{}", book);
    }
}
```

### Key Methods

- `insert`: Adds an element to the set.
- `remove`: Removes an element from the set.
- `contains`: Checks if an element is in the set.

## Summary

Rust's collections provide powerful and flexible ways to manage groups of related data. `Vec`, `HashMap`, and `HashSet` are some of the most commonly used collections in Rust, each with its own strengths and use cases. By understanding and utilizing these collections effectively, you can write more efficient and expressive Rust code.
