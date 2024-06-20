
# Generics in Rust

## Overview

Generics in Rust allow you to write flexible and reusable code by enabling functions, structs, enums, and traits to operate on multiple types of data. Generics are a powerful feature for creating abstractions and ensuring type safety. By using generics, you can define a function, struct, or enum without specifying the exact types it will operate on.

## Generic Functions

You can define functions with generic parameters using angle brackets (`<>`) after the function name. This allows the function to operate on different types.

### Example

```rust
fn largest<T: PartialOrd>(list: &[T]) -> &T {
    let mut largest = &list[0];
    for item in list.iter() {
        if item > largest {
            largest = item;
        }
    }
    largest
}

fn main() {
    let numbers = vec![34, 50, 25, 100, 65];
    let result = largest(&numbers);
    println!("The largest number is {}", result);

    let chars = vec!['y', 'm', 'a', 'q'];
    let result = largest(&chars);
    println!("The largest char is {}", result);
}
```

In this example, the `largest` function can operate on slices of any type that implements the `PartialOrd` trait.

## Generic Structs

You can define structs with generic types to store different types of data.

### Example

```rust
struct Point<T> {
    x: T,
    y: T,
}

fn main() {
    let integer_point = Point { x: 5, y: 10 };
    let float_point = Point { x: 1.0, y: 4.0 };

    println!("integer_point: ({}, {})", integer_point.x, integer_point.y);
    println!("float_point: ({}, {})", float_point.x, float_point.y);
}
```

In this example, the `Point` struct can store values of any type.

## Generic Enums

Enums can also use generics to handle different types of data.

### Example

```rust
enum Option<T> {
    Some(T),
    None,
}

fn main() {
    let some_number = Option::Some(5);
    let some_string = Option::Some("a string");

    println!("{:?}, {:?}", some_number, some_string);
}
```

## Traits with Generics

You can define traits with generic parameters to create more flexible and reusable traits.

### Example

```rust
trait Summary<T> {
    fn summarize(&self) -> T;
}

struct Article {
    title: String,
    content: String,
}

impl Summary<String> for Article {
    fn summarize(&self) -> String {
        format!("{}: {}", self.title, self.content)
    }
}

fn main() {
    let article = Article {
        title: String::from("Rust Generics"),
        content: String::from("Generics allow for flexible and reusable code."),
    };

    println!("Article summary: {}", article.summarize());
}
```

## Generic Constraints

You can specify constraints on generic types using trait bounds to ensure that the types implement specific traits.

### Example

```rust
fn print<T: std::fmt::Display>(item: T) {
    println!("{}", item);
}

fn main() {
    print(42);
    print("Hello, world!");
}
```

In this example, the `print` function requires that the generic type `T` implements the `Display` trait.

## Combining Multiple Traits

You can combine multiple trait bounds using the `+` syntax.

### Example

```rust
fn print_and_return<T: std::fmt::Display + Clone>(item: T) -> T {
    println!("{}", item);
    item.clone()
}

fn main() {
    let value = print_and_return(42);
    println!("Returned value: {}", value);
}
```

## Lifetimes with Generics

Lifetimes are used in conjunction with generics to ensure that references are valid for as long as they are needed.

### Example

```rust
fn longest<'a, T>(x: &'a T, y: &'a T) -> &'a T
where
    T: PartialOrd,
{
    if x > y {
        x
    } else {
        y
    }
}

fn main() {
    let string1 = String::from("long string is long");
    let string2 = String::from("xyz");

    let result = longest(&string1, &string2);
    println!("The longest string is {}", result);
}
```

In this example, the `longest` function ensures that the returned reference is valid for at least as long as the shortest of the input references.

## Summary

Generics in Rust provide a powerful way to write flexible and reusable code. By using generics, you can define functions, structs, enums, and traits that operate on multiple types while maintaining type safety. Understanding how to use generics effectively, along with trait bounds and lifetimes, allows you to create more robust and versatile Rust programs.
