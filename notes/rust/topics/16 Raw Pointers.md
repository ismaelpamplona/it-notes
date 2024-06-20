
# Raw Pointers in Rust

## Overview

Raw pointers in Rust are low-level pointers that provide direct memory access without the safety guarantees enforced by Rust’s borrowing and ownership system. They are used for advanced, low-level programming tasks where you need fine-grained control over memory and performance.

There are two types of raw pointers in Rust:
- `*const T`: An immutable raw pointer.
- `*mut T`: A mutable raw pointer.

## Characteristics of Raw Pointers

1. **No Safety Guarantees**:
   - Raw pointers do not enforce Rust’s safety guarantees. They can lead to undefined behavior if not used correctly.
   
2. **No Automatic Dereferencing**:
   - Unlike references (`&T` and `&mut T`), raw pointers do not automatically dereference. You must manually dereference them within an `unsafe` block.
   
3. **Allow Null Pointers**:
   - Raw pointers can be null, which is not allowed with Rust references.

## Creating Raw Pointers

You can create raw pointers from references using the `as` keyword.

### Example

```rust
fn main() {
    let x = 42;
    let r1 = &x as *const i32; // Immutable raw pointer
    let mut y = 42;
    let r2 = &mut y as *mut i32; // Mutable raw pointer

    unsafe {
        println!("r1 points to: {}", *r1);
        println!("r2 points to: {}", *r2);
    }
}
```

In this example:
- `&x as *const i32` creates an immutable raw pointer to `x`.
- `&mut y as *mut i32` creates a mutable raw pointer to `y`.
- Dereferencing raw pointers must be done within an `unsafe` block.

## Dereferencing Raw Pointers

Dereferencing a raw pointer allows you to access the value it points to. This operation must be done within an `unsafe` block.

### Example

```rust
fn main() {
    let x = 10;
    let y = 20;

    let ptr_x = &x as *const i32;
    let ptr_y = &y as *const i32;

    unsafe {
        println!("Value of x through ptr_x: {}", *ptr_x);
        println!("Value of y through ptr_y: {}", *ptr_y);
    }
}
```

## Null Pointers

Raw pointers can be null, which means they point to no valid memory address.

### Example

```rust
fn main() {
    let ptr: *const i32 = std::ptr::null();
    unsafe {
        if ptr.is_null() {
            println!("ptr is null");
        }
    }
}
```

## Working with Raw Pointers

Raw pointers are often used in FFI (Foreign Function Interface) to interact with C libraries or perform low-level memory operations.

### Example: Interacting with C Code

First, create a C library:

```c
// mylib.c
#include <stdio.h>

void hello_from_c() {
    printf("Hello from C!
");
}
```

Compile the C code:

```sh
gcc -c -fPIC mylib.c -o mylib.o
gcc -shared -o libmylib.so mylib.o
```

Use the C function in Rust:

```rust
extern "C" {
    fn hello_from_c();
}

fn main() {
    unsafe {
        hello_from_c();
    }
}
```

## Summary

Raw pointers in Rust provide powerful capabilities for low-level memory manipulation and interfacing with other programming languages. However, they come with significant risks because they bypass Rust’s safety guarantees. Understanding how to use raw pointers safely and correctly is essential for advanced Rust programming, especially in systems programming and FFI scenarios.

By using raw pointers judiciously within `unsafe` blocks and ensuring proper memory management, you can perform tasks that are not possible with safe Rust while maintaining control over memory and performance.
