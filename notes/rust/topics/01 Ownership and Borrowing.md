# Ownership and Borrowing in Rust

## Overview

Ownership is Rust's unique approach to memory management, which ensures memory safety and eliminates data races. It is enforced through three main rules:

1. Each value in Rust has a variable that is its owner.
2. There can only be one owner at a time.
3. When the owner goes out of scope, the value is dropped.

Borrowing allows you to create references to data without taking ownership, enabling multiple parts of your code to access the same data without violating Rust's safety guarantees.

## Ownership

In Rust, every value has a single owner. When the owner goes out of scope, the value is automatically deallocated. This mechanism is the core of Rust's memory safety model.

### Example

```rust
fn main() {
    let s1 = String::from("hello"); // s1 owns the String
    let s2 = s1; // Ownership of the String is moved to s2
    // s1 is no longer valid and cannot be used
    println!("{}", s2); // This works
    // println!("{}", s1); // This would cause a compile-time error
}
```

In the example above, `s1` is the owner of the `String`. When `s1` is assigned to `s2`, the ownership of the `String` is moved to `s2`, and `s1` is no longer valid.

## Borrowing

Borrowing allows you to create references to a value without taking ownership. There are two types of borrowing:

1. Immutable borrowing (`&T`): Allows read-only access to the data.
2. Mutable borrowing (`&mut T`): Allows read-write access to the data, but only one mutable reference can exist at a time.

### Immutable Borrowing

```rust
fn main() {
    let s = String::from("hello");
    let len = calculate_length(&s); // Borrowing `s` immutably
    println!("The length of '{}' is {}.", s, len);
}

fn calculate_length(s: &String) -> usize {
    s.len() // Use the borrowed value
}
```

In the example above, `&s` is an immutable reference to `s`. The `calculate_length` function borrows `s` without taking ownership, allowing `s` to be used later in the `println!` macro.

### Mutable Borrowing

```rust
fn main() {
    let mut s = String::from("hello");
    change(&mut s); // Borrowing `s` mutably
    println!("{}", s); // `s` can still be used after the mutable borrow
}

fn change(s: &mut String) {
    s.push_str(", world"); // Modify the borrowed value
}
```

In the example above, `&mut s` is a mutable reference to `s`. The `change` function borrows `s` mutably, allowing it to modify the value.

## Rules of Borrowing

1. At any given time, you can have either one mutable reference or any number of immutable references.
2. References must always be valid.

### Example of Borrowing Rules

```rust
fn main() {
    let mut s = String::from("hello");

    let r1 = &s; // No problem
    let r2 = &s; // No problem
    // let r3 = &mut s; // ERROR: cannot borrow `s` as mutable because it is also borrowed as immutable

    println!("{} and {}", r1, r2); // Immutable references are used here

    let r3 = &mut s; // No problem after immutable references are used
    println!("{}", r3);
}
```

In this example, `r1` and `r2` are immutable references to `s`, and they can coexist. However, you cannot have a mutable reference `r3` while `r1` and `r2` are still in scope.

## Summary

Understanding ownership and borrowing is crucial for writing safe and efficient Rust code. Ownership ensures that values have a single owner responsible for their deallocation, while borrowing allows multiple parts of your code to access the same data safely. By following Rust's rules of ownership and borrowing, you can avoid common programming errors such as dangling pointers and data races.

By mastering these concepts, you will be well-prepared to tackle more advanced Rust topics and write high-quality, safe code.
