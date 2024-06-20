# Sync and Send

## Send Trait

The `Send` trait indicates that ownership of the type implementing `Send` can be transferred safely between threads. Almost all primitive types in Rust are `Send`, except for raw pointers.

**Example**:

```rust
use std::thread;

fn main() {
    let v = vec![1, 2, 3];

    let handle = thread::spawn(move || {
        println!("Here's a vector: {:?}", v);
    });

    handle.join().unwrap();
}
```

In this example, the vector `v` is moved into the new thread, demonstrating that `Vec<T>` is `Send`.

## Sync Trait

The `Sync` trait indicates that it is safe for a type implementing `Sync` to be referenced from multiple threads. If `T` is `Sync`, `&T` (a reference to `T`) can be safely shared between threads.

**Example**:

```rust
use std::sync::Arc;
use std::thread;

fn main() {
    let v = Arc::new(vec![1, 2, 3]);
    let v1 = Arc::clone(&v);
    let v2 = Arc::clone(&v);

    let handle1 = thread::spawn(move || {
        println!("Here's a vector: {:?}", v1);
    });

    let handle2 = thread::spawn(move || {
        println!("Here's a vector: {:?}", v2);
    });

    handle1.join().unwrap();
    handle2.join().unwrap();
}
```

In this example, `Arc<T>` is used to share the vector between threads safely. `Arc` is an atomic reference counted pointer that ensures thread-safe reference counting.

## Implementing Sync and Send

Most types in Rust are automatically `Send` and `Sync` if all their components are `Send` and `Sync`. However, you can implement these traits manually for your own types.

**Example of a type implementing Send**:

```rust
struct MyType {
    data: i32,
}

unsafe impl Send for MyType {}

fn main() {
    let my_data = MyType { data: 42 };

    let handle = thread::spawn(move || {
        println!("Data: {}", my_data.data);
    });

    handle.join().unwrap();
}
```

**Example of a type implementing Sync**:

```rust
struct MyType {
    data: i32,
}

unsafe impl Sync for MyType {}

fn main() {
    let my_data = MyType { data: 42 };
    let my_data_ref = &my_data;

    let handle1 = thread::spawn(move || {
        println!("Data: {}", my_data_ref.data);
    });

    let handle2 = thread::spawn(move || {
        println!("Data: {}", my_data_ref.data);
    });

    handle1.join().unwrap();
    handle2.join().unwrap();
}
```

## Ensuring Thread Safety

Rust's type system ensures that data races are prevented at compile time. When using `Send` and `Sync`, Rust guarantees that types implementing these traits can be safely used in concurrent contexts.

**Example**:

```rust
use std::sync::{Mutex, Arc};
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

In this example, `Mutex<T>` is used to ensure mutual exclusion, and `Arc<T>` is used to share ownership safely between threads. The combination of `Arc` and `Mutex` ensures that the counter can be safely incremented by multiple threads without causing data races.
