
# Enums in Rust

## Overview

Enums (short for enumerations) in Rust allow you to define a type by enumerating its possible variants. Enums are powerful for modeling data that can take on a fixed set of states, providing a way to handle multiple related values in a type-safe manner. Enums in Rust can also hold data, making them even more versatile.

## Defining Enums

You define an enum using the `enum` keyword, followed by the name of the enum and a list of its possible variants.

### Example

```rust
enum IpAddrKind {
    V4,
    V6,
}

fn main() {
    let four = IpAddrKind::V4;
    let six = IpAddrKind::V6;

    route(four);
    route(six);
}

fn route(ip_kind: IpAddrKind) {
    match ip_kind {
        IpAddrKind::V4 => println!("IPv4 address"),
        IpAddrKind::V6 => println!("IPv6 address"),
    }
}
```

## Enums with Data

Enums in Rust can also contain data, making them similar to algebraic data types in functional programming languages.

### Example

```rust
enum IpAddr {
    V4(String),
    V6(String),
}

fn main() {
    let home = IpAddr::V4(String::from("127.0.0.1"));
    let loopback = IpAddr::V6(String::from("::1"));

    println!("Home address: {:?}", home);
    println!("Loopback address: {:?}", loopback);
}
```

In this example, each variant of the `IpAddr` enum can hold a `String` value.

## Enums with Different Types of Data

Enums can also hold different types of data in each variant.

### Example

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

fn main() {
    let quit = Message::Quit;
    let move_message = Message::Move { x: 10, y: 20 };
    let write_message = Message::Write(String::from("hello"));
    let change_color = Message::ChangeColor(255, 0, 0);

    println!("{:?}, {:?}, {:?}, {:?}", quit, move_message, write_message, change_color);
}
```

## Using Enums with `match`

The `match` expression in Rust is used to handle different variants of an enum, providing a concise way to execute different code based on the variant.

### Example

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

fn main() {
    let msg = Message::Move { x: 10, y: 20 };

    match msg {
        Message::Quit => println!("Quit"),
        Message::Move { x, y } => println!("Move to x: {}, y: {}", x, y),
        Message::Write(text) => println!("Write: {}", text),
        Message::ChangeColor(r, g, b) => println!("Change color to red: {}, green: {}, blue: {}", r, g, b),
    }
}
```

## The `Option` Enum

The `Option` enum is a powerful enum provided by the Rust standard library to handle cases where a value can be either something or nothing. It is defined as:

```rust
enum Option<T> {
    Some(T),
    None,
}
```

### Example

```rust
fn main() {
    let some_number = Some(5);
    let some_string = Some("a string");

    let absent_number: Option<i32> = None;

    println!("{:?}, {:?}, {:?}", some_number, some_string, absent_number);
}
```

## The `Result` Enum

The `Result` enum is another powerful enum provided by the Rust standard library to handle operations that can either succeed or fail. It is defined as:

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

### Example

```rust
use std::fs::File;
use std::io::ErrorKind;

fn main() {
    let greeting_file_result = File::open("hello.txt");

    match greeting_file_result {
        Ok(file) => println!("File opened successfully: {:?}", file),
        Err(error) => match error.kind() {
            ErrorKind::NotFound => println!("File not found"),
            other_error => println!("Error opening file: {:?}", other_error),
        },
    }
}
```

## Summary

Enums in Rust are a powerful feature that allows you to define a type by enumerating its possible variants. Enums can hold data, including different types of data, making them versatile for modeling various situations. Using enums with `match` expressions provides a concise and type-safe way to handle different states. The `Option` and `Result` enums in the standard library are particularly useful for handling cases of optional values and error handling.
