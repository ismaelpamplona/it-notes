# Structs, Traits, Enums

## Structs

In Rust, a `struct` is a custom data type that lets you name and package together multiple related values. Structs are a way to create more complex data types than those provided by the standard library.

Example:

```rust
struct User {
    username: String,
    email: String,
    sign_in_count: u64,
    active: bool,
}

fn main() {
    let user1 = User {
        email: String::from("someone@example.com"),
        username: String::from("someusername123"),
        active: true,
        sign_in_count: 1,
    };

    println!("Username: {}", user1.username);
}
```

## Traits

Traits in Rust are similar to interfaces in other languages. They allow you to define shared behavior in an abstract way.

Example:

```rust
trait Summary {
    fn summarize(&self) -> String;
}

struct Article {
    headline: String,
    location: String,
    author: String,
    content: String,
}

impl Summary for Article {
    fn summarize(&self) -> String {
        format!("{}, by {} ({})", self.headline, self.author, self.location)
    }
}

fn main() {
    let article = Article {
        headline: String::from("Rust is Great!"),
        location: String::from("The Internet"),
        author: String::from("John Doe"),
        content: String::from("Rust is a systems programming language..."),
    };

    println!("New article available! {}", article.summarize());
}
```

## Enums

Enums allow you to define a type by enumerating its possible values.

Example:

```rust
enum IpAddrKind {
    V4,
    V6,
}

struct IpAddr {
    kind: IpAddrKind,
    address: String,
}

fn main() {
    let home = IpAddr {
        kind: IpAddrKind::V4,
        address: String::from("127.0.0.1"),
    };

    let loopback = IpAddr {
        kind: IpAddrKind::V6,
        address: String::from("::1"),
    };

    println!("IP Address 1: {:?}", home);
    println!("IP Address 2: {:?}", loopback);
}
```

## Copy Trait

The `Copy` trait in Rust allows for types that can be duplicated simply by copying bits.

Example:

```rust
#[derive(Copy, Clone)]
struct Point {
    x: i32,
    y: i32,
}

fn main() {
    let p1 = Point { x: 0, y: 0 };
    let p2 = p1;

    println!("p1: ({}, {}), p2: ({}, {})", p1.x, p1.y, p2.x, p2.y);
}
```

## Clone Trait

The `Clone` trait allows for explicit duplication of data.

Example:

```rust
#[derive(Clone)]
struct Person {
    name: String,
    age: u8,
}

fn main() {
    let person1 = Person {
        name: String::from("Alice"),
        age: 30,
    };

    let person2 = person1.clone();

    println!("Person 1: {} is {} years old", person1.name, person1.age);
    println!("Person 2: {} is {} years old", person2.name, person2.age);
}
```

## Sync and Send

`Sync` and `Send` are marker traits that are related to concurrency.

- `Send` indicates that ownership of the type implementing `Send` can be transferred between threads.
- `Sync` indicates that it is safe for the type implementing `Sync` to be referenced from multiple threads.

Example:

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

In this example, the vector `v` is moved into the new thread, demonstrating `Send`.

### Sync Example

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

In this example, `Arc` is used to safely share the vector between threads, demonstrating `Sync`.
