# Concurrency in Rust

## Overview

Concurrency in Rust allows you to write programs that can perform multiple tasks simultaneously, making efficient use of system resources. Rust's ownership system and concurrency primitives, such as threads, channels, and the `async`/`await` model, ensure safe and efficient concurrent execution. This ensures that your concurrent programs are free from data races and other concurrency-related issues.

## Threads

Rust's standard library provides support for creating and managing threads. Each thread runs concurrently with other threads, allowing you to perform multiple tasks simultaneously.

### Example

```rust
use std::thread;

fn main() {
    let handle = thread::spawn(|| {
        for i in 1..10 {
            println!("Hi number {} from the spawned thread!", i);
            thread::sleep(std::time::Duration::from_millis(1));
        }
    });

    for i in 1..5 {
        println!("Hi number {} from the main thread!", i);
        thread::sleep(std::time::Duration::from_millis(1));
    }

    handle.join().unwrap();
}
```

In this example:

- `thread::spawn` creates a new thread and runs the closure in it.
- `handle.join()` ensures that the main thread waits for the spawned thread to finish.

## Channels

Channels provide a way for threads to communicate with each other. Rust’s standard library includes channels for message passing between threads.

### Example

```rust
use std::sync::mpsc;
use std::thread;
use std::time::Duration;

fn main() {
    let (tx, rx) = mpsc::channel();

    thread::spawn(move || {
        let val = String::from("hi");
        tx.send(val).unwrap();
    });

    let received = rx.recv().unwrap();
    println!("Got: {}", received);
}
```

In this example:

- `mpsc::channel` creates a channel with a transmitter (`tx`) and a receiver (`rx`).
- The spawned thread sends a message through the transmitter.
- The main thread receives the message through the receiver.

## `async`/`await`

The `async`/`await` syntax in Rust allows you to write asynchronous code that looks like synchronous code. This model is particularly useful for I/O-bound tasks.

### Example

```rust
use tokio::time::{sleep, Duration};

#[tokio::main]
async fn main() {
    let handle = tokio::spawn(async {
        for i in 1..10 {
            println!("Hi number {} from the spawned async task!", i);
            sleep(Duration::from_millis(1)).await;
        }
    });

    for i in 1..5 {
        println!("Hi number {} from the main async task!", i);
        sleep(Duration::from_millis(1)).await;
    }

    handle.await.unwrap();
}
```

In this example:

- `tokio::spawn` creates a new asynchronous task.
- `sleep` is an asynchronous function that simulates work by sleeping for a specified duration.

## Synchronization Primitives

Rust provides several synchronization primitives to manage concurrent access to shared data. These include `Mutex`, `RwLock`, and `Arc`.

### `Mutex`

A `Mutex` allows you to enforce mutual exclusion, ensuring that only one thread can access the data at a time.

### Example

```rust
use std::sync::{Arc, Mutex};
use std::thread;

fn main() {
    let counter = Arc::new(Mutex::new(0));
    let mut handles = vec![];

    for _ in 0..10 {
        let counter = Arc::clone(&counter);
        let handle = thread::spawn(move || {
            let mut num = counter.lock().unwrap();
            *num += 1;
        });
        handles.push(handle);
    }

    for handle in handles {
        handle.join().unwrap();
    }

    println!("Result: {}", *counter.lock().unwrap());
}
```

In this example:

- `Arc` is used to share ownership of the `Mutex` across multiple threads.
- `Mutex` ensures that only one thread can access the counter at a time.

## `RwLock`

An `RwLock` allows multiple readers or a single writer to access the data. It is more efficient than a `Mutex` when reads are more frequent than writes.

### One single writer

```rust
use std::sync::{Arc, RwLock};
use std::thread;

fn main() {
    let data = Arc::new(RwLock::new(5));
    let mut handles = vec![];

    for _ in 0..10 {
        let data = Arc::clone(&data);
        let handle = thread::spawn(move || {
            let mut write_data = data.write().unwrap();
            *write_data += 1;
        });
        handles.push(handle);
    }

    for handle in handles {
        handle.join().unwrap();
    }

    let read_data = data.read().unwrap();
    println!("Result: {}", *read_data);
}
```

In this example:

- `Arc` is used to share ownership of the `RwLock` across multiple threads.
- `RwLock` allows either multiple readers or a single writer, optimizing access patterns.

### Multiple readers

```rust
use std::sync::{Arc, RwLock};
use std::thread;

fn main() {
    // Create an RwLock wrapped in an Arc for shared ownership
    let data = Arc::new(RwLock::new(5));

    let mut handles = vec![];

    // Spawn multiple reader threads
    for i in 0..5 {
        let data = Arc::clone(&data);
        let handle = thread::spawn(move || {
            // Acquire a read lock
            let read_data = data.read().unwrap();
            println!("Reader {}: {}", i, *read_data);
        });
        handles.push(handle);
    }

    // Join all the threads
    for handle in handles {
        handle.join().unwrap();
    }

    // Check final value
    println!("Final value: {}", *data.read().unwrap());
}

```

## Summary

Concurrency in Rust is facilitated by a combination of threads, channels, `async`/`await`, and synchronization primitives like `Mutex` and `RwLock`. Rust's ownership and borrowing rules ensure that concurrent programs are free from data races and other concurrency-related issues, making it possible to write safe and efficient concurrent code.
