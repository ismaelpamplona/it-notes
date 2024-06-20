# Error Handling in Rust

## Overview

Error handling in Rust is designed to be safe and explicit, reducing the chances of runtime crashes and making it clear when a function can fail. Rust uses two main types for error handling: `Result` and `Option`. The `Result` type is used for functions that can return a value or an error, while the `Option` type is used for values that may or may not be present.

## The `Result` Type

The `Result` type is an enum that can be either `Ok` or `Err`. It is used for functions that can succeed or fail. The `Result` type is defined as:

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

- `T`: The type of the value returned in the success case.
- `E`: The type of the error returned in the failure case.

### Example

```rust
fn divide(dividend: f64, divisor: f64) -> Result<f64, String> {
    if divisor == 0.0 {
        Err(String::from("Cannot divide by zero"))
    } else {
        Ok(dividend / divisor)
    }
}

fn main() {
    match divide(10.0, 2.0) {
        Ok(result) => println!("Result: {}", result),
        Err(e) => println!("Error: {}", e),
    }

    match divide(10.0, 0.0) {
        Ok(result) => println!("Result: {}", result),
        Err(e) => println!("Error: {}", e),
    }
}
```

### Using `?` Operator

The `?` operator provides a concise way to propagate errors. It can be used in functions that return a `Result` or `Option`.

```rust
fn read_file(filename: &str) -> Result<String, io::Error> {
    let mut file = File::open(filename)?;
    let mut contents = String::new();
    file.read_to_string(&mut contents)?;
    Ok(contents)
}
```

In this example, if `File::open` or `file.read_to_string` fails, the error is returned from `read_file` immediately.

## The `Option` Type

The `Option` type is used when a value might be absent. It is an enum with two variants: `Some` and `None`.

```rust
enum Option<T> {
    Some(T),
    None,
}
```

- `T`: The type of the value that might be present.

### Example

```rust
fn find_number(numbers: &[i32], target: i32) -> Option<usize> {
    for (index, &number) in numbers.iter().enumerate() {
        if number == target {
            return Some(index);
        }
    }
    None
}

fn main() {
    let numbers = vec![1, 2, 3, 4, 5];
    match find_number(&numbers, 3) {
        Some(index) => println!("Found at index: {}", index),
        None => println!("Not found"),
    }

    match find_number(&numbers, 6) {
        Some(index) => println!("Found at index: {}", index),
        None => println!("Not found"),
    }
}
```

### Handling Errors Gracefully

Using `Result` and `Option`, you can handle errors gracefully without panicking. This makes your code more robust and user-friendly.

#### Example with `unwrap_or`

```rust
fn main() {
    let result = divide(10.0, 0.0).unwrap_or(f64::INFINITY);
    println!("Result: {}", result);
}
```

In this example, `unwrap_or` provides a default value if the `Result` is `Err`.

## Custom Error Types

You can define custom error types to provide more context about failures.

### Example

```rust
use std::fmt;

#[derive(Debug)]
enum MathError {
    DivisionByZero,
    NegativeLogarithm,
}

impl fmt::Display for MathError {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        match *self {
            MathError::DivisionByZero => write!(f, "Cannot divide by zero"),
            MathError::NegativeLogarithm => {
                write!(f, "Cannot compute the logarithm of a negative number")
            }
        }
    }
}

fn divide(dividend: f64, divisor: f64) -> Result<f64, MathError> {
    if divisor == 0.0 {
        return Err(MathError::DivisionByZero);
    }
    Ok(dividend / divisor)
}

fn main() {
    match divide(10.0, 0.0) {
        Ok(result) => println!("Result: {}", result),
        Err(e) => println!("Error: {}", e),
    }
}
```

## Summary

Error handling in Rust is explicit and type-safe, preventing many common programming errors. The `Result` and `Option` types allow you to handle errors gracefully, making your code robust and reliable. The `?` operator simplifies error propagation, while custom error types provide context-specific error messages. Mastering Rust's error handling mechanisms will enable you to write resilient and user-friendly applications.
