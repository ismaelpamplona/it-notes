
# Difference Between `const` and `static` in Rust

## Overview

In Rust, both `const` and `static` can be used to define constants, but they have distinct differences in terms of their behavior and usage.

## `const`

- **Definition**: Defines a constant value that is inlined wherever it is used.
- **Evaluation**: Evaluated at compile time.
- **Memory Allocation**: Does not allocate memory. The value is directly embedded into the code wherever it is used.
- **Usage**: Typically used for values that are known at compile time and do not need a fixed memory address.
- **Scope**: Limited to the scope in which they are declared, but can be made public for broader access.
- **Mutability**: Always immutable.

### Example

```rust
const MY_VAR: i32 = 0;

fn main() {
    println!("The value of MY_VAR is {}", MY_VAR);
}
```

### Characteristics of `const`

- **Inlined**: The value of `MY_VAR` is directly embedded into the code at every point it is used.
- **No Memory Address**: `const` does not have a fixed memory address because it is inlined.

## `static`

- **Definition**: Defines a global variable with a fixed memory address.
- **Evaluation**: Initialized at compile time, but the value has a fixed memory address at runtime.
- **Memory Allocation**: Allocates memory to store the value.
- **Usage**: Typically used for global state that requires a fixed memory address, such as global variables or when interfacing with other programming languages.
- **Scope**: Global by default, but can be restricted with visibility modifiers.
- **Mutability**: Can be mutable if declared with `static mut`, but this requires careful handling to avoid undefined behavior.

### Example

```rust
static MY_VAR: i32 = 0;

fn main() {
    println!("The value of MY_VAR is {}", MY_VAR);
}
```

### Characteristics of `static`

- **Fixed Memory Address**: `MY_VAR` has a fixed memory address, meaning it is stored at a specific location in memory.
- **Global Scope**: Accessible from any part of the program, similar to a global variable.

## Comparison

| Feature          | `const`                        | `static`                        |
|------------------|--------------------------------|---------------------------------|
| Definition       | Compile-time constant          | Global variable                 |
| Evaluation       | Compile time                   | Compile time, with fixed address|
| Memory Allocation| None (inlined)                 | Allocated memory                |
| Mutability       | Always immutable               | Mutable with `static mut`       |
| Usage            | Constants, inlined values      | Global state, interfacing with other languages |
| Scope            | Scoped, but can be public      | Global, but can be restricted   |

## When to Use Each

- **Use `const`**:
  - When you need a compile-time constant.
  - When the value does not need a fixed memory address.
  - When you want the value to be inlined.

- **Use `static`**:
  - When you need a global variable with a fixed memory address.
  - When interfacing with other programming languages that require global variables.
  - When you need to store data that persists for the entire duration of the program.

## Summary

- `const` is for compile-time constants that are inlined and do not allocate memory.
- `static` is for global variables that have a fixed memory address and can optionally be mutable. 

Understanding the differences between `const` and `static` helps in choosing the right type of constant for your use case in Rust.
