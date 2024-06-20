
# Rust's Module System

## Overview

Rust's module system allows you to organize your code into separate namespaces, making it easier to manage and maintain. Modules can group related functions, structs, traits, and other items together, promoting code reuse and modularity. The module system in Rust also supports privacy rules, making it possible to hide implementation details while exposing a clean public API.

## Creating Modules

Modules in Rust can be created using the `mod` keyword. You can define modules inline or in separate files.

### Inline Modules

```rust
mod outer {
    pub mod inner {
        pub fn greet() {
            println!("Hello from the inner module!");
        }
    }
}

fn main() {
    outer::inner::greet();
}
```

### Modules in Separate Files

You can organize your modules into separate files for better code organization.

#### Directory Structure

```
src/
 ├── main.rs
 └── outer/
     ├── mod.rs
     └── inner.rs
```

#### main.rs

```rust
mod outer;

fn main() {
    outer::inner::greet();
}
```

#### outer/mod.rs

```rust
pub mod inner;
```

#### outer/inner.rs

```rust
pub fn greet() {
    println!("Hello from the inner module!");
}
```

## Privacy

Rust's module system enforces privacy rules to control the visibility of code. By default, everything in a module is private. You can use the `pub` keyword to make items public.

### Example

```rust
mod outer {
    pub mod inner {
        pub fn greet() {
            println!("Hello from the inner module!");
        }

        fn secret() {
            println!("This is a secret function.");
        }
    }
}

fn main() {
    outer::inner::greet();
    // outer::inner::secret(); // Error: function `secret` is private
}
```

In this example:
- `greet` is public and can be accessed from outside the `inner` module.
- `secret` is private and cannot be accessed from outside the `inner` module.

## Using `use` for Importing

The `use` keyword allows you to bring module paths into scope, making them easier to reference.

### Example

```rust
mod outer {
    pub mod inner {
        pub fn greet() {
            println!("Hello from the inner module!");
        }
    }
}

use outer::inner::greet;

fn main() {
    greet();
}
```

In this example, `use outer::inner::greet` brings the `greet` function into scope, allowing you to call it directly.

## Nested Modules

Modules can be nested to create a hierarchy, helping to further organize code.

### Example

```rust
mod outer {
    pub mod middle {
        pub mod inner {
            pub fn greet() {
                println!("Hello from the inner module!");
            }
        }
    }
}

fn main() {
    outer::middle::inner::greet();
}
```

## Re-exporting

You can re-export items to make them available at a higher module level.

### Example

```rust
mod outer {
    pub mod inner {
        pub fn greet() {
            println!("Hello from the inner module!");
        }
    }

    pub use inner::greet;
}

fn main() {
    outer::greet();
}
```

In this example, `greet` is re-exported from the `inner` module to the `outer` module, allowing it to be accessed as `outer::greet`.

## Advanced Module Features

### Module Visibility

By default, modules are private. You can make a module public by using the `pub` keyword.

#### Example

```rust
pub mod outer {
    pub mod inner {
        pub fn greet() {
            println!("Hello from the inner module!");
        }
    }
}
```

### Path Resolution

Rust uses a tree structure for module resolution. Use `super::` to refer to the parent module and `self::` to refer to the current module.

#### Example

```rust
mod outer {
    pub mod inner {
        pub fn greet() {
            super::announce();
        }
    }

    pub fn announce() {
        println!("This is the outer module!");
    }
}

fn main() {
    outer::inner::greet();
}
```

### Crate Root

The crate root is the source file that the Rust compiler starts from and makes up the root module of your crate. By default, this is `src/main.rs` for a binary crate and `src/lib.rs` for a library crate.

### Example of Crate Root

#### lib.rs

```rust
pub mod outer;
```

#### outer/mod.rs

```rust
pub mod inner;

pub fn announce() {
    println!("This is the outer module!");
}
```

#### outer/inner.rs

```rust
pub fn greet() {
    println!("Hello from the inner module!");
}
```

#### Usage in main.rs

```rust
use my_crate::outer::inner::greet;
use my_crate::outer::announce;

fn main() {
    greet();
    announce();
}
```

## Summary

Rust's module system provides a powerful way to organize code into namespaces, enforce privacy, and manage dependencies. By using modules, you can create clean, maintainable, and reusable code structures. Understanding how to create and use modules, control visibility, re-export items, and leverage advanced features will help you write more modular and organized Rust programs.
