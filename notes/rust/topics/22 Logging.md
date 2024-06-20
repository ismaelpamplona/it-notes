
# Logging in Rust

Logging is essential for understanding the behavior of your application, especially in production environments. Rust provides several libraries for logging, with `log` and `env_logger` being the most commonly used. This guide will walk you through setting up and using logging in a Rust application.

## Step 1: Setup the Project

First, create a new Rust project:

```sh
cargo new logging_example
cd logging_example
```

Add the dependencies in `Cargo.toml`:

```toml
[dependencies]
log = "0.4"
env_logger = "0.9"
```

## Step 2: Implement Logging

Create a `src/main.rs` file with the following content:

```rust
use log::{debug, error, info, trace, warn};
use env_logger::Env;

fn main() {
    // Initialize the logger with environment variable support
    env_logger::init_from_env(Env::default().default_filter_or("info"));

    info!("Starting the application");
    debug!("This is a debug message");
    warn!("This is a warning message");
    error!("This is an error message");

    let result = some_function(42);
    trace!("The result of some_function is: {:?}", result);
}

fn some_function(value: i32) -> i32 {
    info!("Calling some_function with value: {}", value);
    value * 2
}
```

## Explanation

1. **Dependencies**:
    - `log`: Provides macros for logging at different levels (trace, debug, info, warn, error).
    - `env_logger`: Initializes logging based on environment variables.

2. **Initialization**:
    - `env_logger::init_from_env(Env::default().default_filter_or("info"));`: Initializes the logger and sets the default log level to `info`. You can override this by setting the `RUST_LOG` environment variable.

3. **Logging Macros**:
    - `trace!`, `debug!`, `info!`, `warn!`, `error!`: Macros provided by the `log` crate to log messages at different levels.

4. **Function Logging**:
    - `some_function`: Demonstrates logging within a function.

## Running the Application

Run the application using:

```sh
cargo run
```

By default, you will see logs at the `info`, `warn`, and `error` levels. To change the log level, set the `RUST_LOG` environment variable:

```sh
RUST_LOG=trace cargo run
```

This will enable all log levels, including `debug` and `trace`.

