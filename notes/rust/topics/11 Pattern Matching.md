# Pattern Matching in Rust

## Overview

Pattern matching is a powerful feature in Rust that allows you to destructure and match complex data types, enabling concise and expressive code. It is used extensively with `match` statements, `if let`, `while let`, and other constructs. Pattern matching helps you write more readable and maintainable code by handling different cases explicitly.

## Match Statement

The `match` statement in Rust is used to compare a value against a series of patterns and execute code based on which pattern matches. Each arm of a `match` statement consists of a pattern and the code to run if the value matches that pattern.

### Example

```rust
fn main() {
    let number = 13;

    match number {
        1 => println!("One"),
        2 => println!("Two"),
        3..=12 => println!("Three to Twelve"),
        13 => println!("Thirteen"),
        _ => println!("Other"),
    }
}
```

In this example:

- `1`, `2`, and `13` are specific patterns.
- `3..=12` is a range pattern.
- `_` is a catch-all pattern that matches any value not covered by the previous patterns.

## Destructuring

Pattern matching can destructure complex data types like tuples, structs, and enums.

### Tuples

```rust
fn main() {
    let pair = (0, -2);

    match pair {
        (0, y) => println!("First is 0 and y is {}", y),
        (x, 0) => println!("x is {} and second is 0", x),
        _ => println!("It doesn't matter what they are"),
    }
}
```

### Structs

```rust
struct Point {
    x: i32,
    y: i32,
}

fn main() {
    let point = Point { x: 0, y: 7 };

    match point {
        Point { x: 0, y } => println!("On the y axis at {}", y),
        Point { x, y: 0 } => println!("On the x axis at {}", x),
        Point { x, y } => println!("On neither axis: ({}, {})", x, y),
    }
}
```

### Enums

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

fn main() {
    let msg = Message::Move { x: 1, y: 3 };

    match msg {
        Message::Quit => println!("The Quit variant has no data to destructure."),
        Message::Move { x, y } => println!("Move in the x direction {} and in the y direction {}", x, y),
        Message::Write(text) => println!("Text message: {}", text),
        Message::ChangeColor(r, g, b) => println!("Change the color to red {}, green {}, and blue {}", r, g, b),
    }
}
```

## `if let` and `while let`

`if let` and `while let` are used to match patterns in a concise way for single pattern matching.

### `if let`

```rust
fn main() {
    let favorite_color: Option<&str> = Some("blue");

    if let Some(color) = favorite_color {
        println!("Favorite color is {}", color);
    } else {
        println!("No favorite color");
    }
}
```

### `while let`

```rust
fn main() {
    let mut stack = Vec::new();

    stack.push(1);
    stack.push(2);
    stack.push(3);

    while let Some(top) = stack.pop() {
        println!("{}", top);
    }
}
```

## Refutability

Patterns in Rust can be refutable or irrefutable. Refutable patterns can fail to match, while irrefutable patterns always match.

### Example of Refutable and Irrefutable Patterns

```rust
fn main() {
    let some_option_value: Option<i32> = None;

    // if let expects a refutable pattern
    if let Some(x) = some_option_value {
        println!("Matched: {}", x);
    } else {
        println!("Did not match");
    }

    // let expects an irrefutable pattern
    let (a, b, c) = (1, 2, 3); // This will always match
    println!("a: {}, b: {}, c: {}", a, b, c);
}
```

## Pattern Matching with Guards

Pattern guards allow you to add additional conditions to patterns.

### Example

```rust
fn main() {
    let num = Some(4);

    match num {
        Some(x) if x < 5 => println!("Less than five: {}", x),
        Some(x) => println!("{}", x),
        None => (),
    }
}
```

## Summary

Pattern matching in Rust is a versatile feature that enables concise and expressive handling of different data structures and conditions. Using `match` statements, destructuring, `if let`, `while let`, and pattern guards, you can write clear and maintainable code that explicitly handles various cases.
