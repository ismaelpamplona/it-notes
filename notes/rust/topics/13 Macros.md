# Macros in Rust

## Overview

Macros in Rust allow you to write code that generates other code, enabling metaprogramming. They help reduce boilerplate, create domain-specific languages (DSLs), and extend the language in powerful ways. Rust provides two main types of macros: declarative macros (using `macro_rules!`) and procedural macros.

## Declarative Macros

Declarative macros are defined using the `macro_rules!` syntax. These macros are more like pattern matching, where you define rules to match against the input and generate the corresponding output.

### Example

```rust
macro_rules! say_hello {
    () => {
        println!("Hello!");
    };
}

fn main() {
    say_hello!(); // Expands to println!("Hello!");
}
```

### Example with Parameters

```rust
macro_rules! create_function {
    ($func_name:ident) => {
        fn $func_name() {
            println!("You called {}()", stringify!($func_name));
        }
    };
}

create_function!(foo);
create_function!(bar);

fn main() {
    foo();
    bar();
}
```

## Procedural Macros

Procedural macros are more complex and powerful. They operate on the abstract syntax tree (AST) of the code, allowing more flexibility. Procedural macros are defined using attributes such as `#[derive]`, `#[proc_macro]`, `#[proc_macro_derive]`, and `#[proc_macro_attribute]`.

### Custom Derive Macro

Custom derive macros allow you to implement traits for structs or enums automatically.

#### Example

```rust
// In your crate's lib.rs
use proc_macro::TokenStream;
use quote::quote;
use syn;

#[proc_macro_derive(HelloMacro)]
pub fn hello_macro_derive(input: TokenStream) -> TokenStream {
    let ast = syn::parse(input).unwrap();
    impl_hello_macro(&ast)
}

fn impl_hello_macro(ast: &syn::DeriveInput) -> TokenStream {
    let name = &ast.ident;
    let gen = quote! {
        impl HelloMacro for #name {
            fn hello() {
                println!("Hello, Macro! My name is {}!", stringify!(#name));
            }
        }
    };
    gen.into()
}
```

#### Usage

```rust
use hello_macro::HelloMacro;

#[derive(HelloMacro)]
struct Pancakes;

fn main() {
    Pancakes::hello();
}
```

## Attribute Macros

Attribute macros allow you to create custom attributes that you can apply to items in your code.

### Example

```rust
use proc_macro::TokenStream;

#[proc_macro_attribute]
pub fn route(attr: TokenStream, item: TokenStream) -> TokenStream {
    let attr = attr.to_string();
    let item = item.to_string();
    let output = format!("fn {} {{ println!("Route: {}"); {} }}", item, attr, item);
    output.parse().unwrap()
}
```

### Usage

```rust
#[route(GET)]
fn get_index() {
    println!("This is the index");
}
```

## Function-like Macros

Function-like macros are similar to declarative macros but use a different syntax. They are defined using the `#[proc_macro]` attribute.

### Example

```rust
use proc_macro::TokenStream;

#[proc_macro]
pub fn my_macro(input: TokenStream) -> TokenStream {
    let input = input.to_string();
    let output = format!("fn generated() {{ println!("{}"); }}", input);
    output.parse().unwrap()
}
```

### Usage

```rust
my_macro!("Hello, world!");

fn main() {
    generated();
}
```

## Summary

Macros in Rust provide powerful metaprogramming capabilities that help reduce boilerplate, create DSLs, and extend the language. Declarative macros (`macro_rules!`) offer pattern-based code generation, while procedural macros provide more flexibility by operating on the AST. Understanding and leveraging macros can significantly enhance your Rust programming experience, allowing you to write more concise, expressive, and maintainable code.
