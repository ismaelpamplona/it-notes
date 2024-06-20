# Unsafe Rust

## Overview

Unsafe Rust allows you to perform low-level programming tasks that are not checked by the Rust compiler’s safety guarantees. This includes direct memory manipulation, calling unsafe functions, and interfacing with other programming languages through FFI (Foreign Function Interface). Using `unsafe` code requires careful handling to avoid undefined behavior and potential security vulnerabilities.

## Unsafe Blocks

Unsafe operations in Rust must be enclosed in `unsafe` blocks. This tells the compiler that you are aware of the potential risks and are taking responsibility for ensuring safety.

### Example

```rust
fn main() {
    let mut num = 5;

    let r1 = &num as *const i32; // Raw pointer to const i32
    let r2 = &mut num as *mut i32; // Raw pointer to mut i32

    unsafe {
        println!("r1 is: {}", *r1);
        println!("r2 is: {}", *r2);
    }
}
```

In this example:

- `&num as *const i32` and `&mut num as *mut i32` create raw pointers.
- Dereferencing raw pointers is only allowed within an `unsafe` block.

## Unsafe Functions

Functions can be declared as `unsafe` if they perform unsafe operations. Calling these functions also requires an `unsafe` block.

### Example

```rust
unsafe fn dangerous() {
    // Perform some unsafe operations
}

fn main() {
    unsafe {
        dangerous();
    }
}
```

## Dereferencing Raw Pointers

Raw pointers (`*const T` and `*mut T`) can be used for low-level memory manipulation but are inherently unsafe because they can lead to undefined behavior if not handled correctly.

### Example

```rust
fn main() {
    let mut num = 42;

    let r1 = &num as *const i32;
    let r2 = &mut num as *mut i32;

    unsafe {
        println!("r1 points to: {}", *r1);
        *r2 = 13;
        println!("r2 points to: {}", *r2);
    }
}
```

## Calling Unsafe Functions or Methods

Standard library functions that are unsafe can only be called within an `unsafe` block.

### Example

```rust
fn main() {
    let mut v = vec![1, 2, 3, 4, 5];

    let ptr = v.as_mut_ptr(); // Get a raw mutable pointer to the vector's buffer
    let len = v.len();

    unsafe {
        for i in 0..len {
            println!("{}", *ptr.add(i));
        }
    }
}
```

## External Functions (FFI)

Rust allows you to call functions from other languages (like C) using the Foreign Function Interface (FFI). These functions are inherently unsafe because Rust cannot guarantee their safety.

### Example

First, create a C library with the following function:

```c
// mylib.c
#include <stdio.h>

void hello_from_c() {
    printf("Hello from C!
");
}
```

Compile the C code into a shared library:

```sh
gcc -c -fPIC mylib.c -o mylib.o
gcc -shared -o libmylib.so mylib.o
```

Then, use the C function in Rust:

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

## Accessing and Modifying Static Variables

Static variables can be accessed and modified within an `unsafe` block.

### Example

```rust
static mut COUNTER: u32 = 0;

fn add_to_counter(inc: u32) {
    unsafe {
        COUNTER += inc;
    }
}

fn main() {
    add_to_counter(3);

    unsafe {
        println!("COUNTER: {}", COUNTER);
    }
}
```

## Unsafe Traits

Traits can be marked as `unsafe` if they have methods that are unsafe to implement or call.

### Example

```rust
unsafe trait UnsafeTrait {
    // Methods go here
}

unsafe impl UnsafeTrait for i32 {
    // Implementation goes here
}
```

## Summary

Unsafe Rust provides powerful capabilities for low-level programming, but it requires careful handling to avoid undefined behavior and security issues. By using `unsafe` blocks, functions, raw pointers, FFI, and other unsafe features judiciously, you can perform tasks that are not possible in safe Rust while maintaining control over memory safety and concurrency. Understanding when and how to use unsafe code is crucial for advanced Rust programming, especially in systems programming and interfacing with other languages.
