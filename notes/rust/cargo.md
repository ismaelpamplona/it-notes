# Cargo

## How to shows the result of macro expansion and `#[derive]` expansion?

Install `cargo-expand`:

```bash
cargo install cargo-expand.
```

Once installed, the following command prints out the result of macro expansion and #[derive] expansion applied to the current crate.

```bash
$ cargo expand
```

Open the expanded code directly on VSCode

```bash
cargo expand | code -
```

## How to test your code?

```console
$ cargo test -p <lib_name> -- --nocapture
```

- `--` is used as a separator to distinguish between the arguments
- `--nocapture` indicates that the output of the test cases should not be captured, and thus, should be displayed regardless of whether the test passes or fails.

## How to run Clippy linting tool?

```console
$ cargo clippy -p <lib_name>
```
