# Publishing a Rust CLI App in Ubuntu and Debian

Publishing a Rust CLI app for Ubuntu and Debian involves creating a `.deb` package, which can then be distributed and installed on systems using these distributions. Here's a step-by-step guide:

## Step 1: Prepare Your Rust Project

Ensure that your Rust project is ready for distribution. This includes having a `Cargo.toml` file and a compiled binary.

1. **Initialize your project**:

   ```bash
   cargo new my_cli_app
   cd my_cli_app
   ```

2. **Build your project**:
   ```bash
   cargo build --release
   ```

## Step 2: Install Necessary Tools

You need to install `cargo-deb`, a tool for creating Debian packages from Rust projects.

```bash
cargo install cargo-deb
```

## Step 3: Create a `Cargo.toml` File

Ensure your `Cargo.toml` file includes necessary metadata for creating the `.deb` package.

```toml
[package]
name = "my_cli_app"
version = "0.1.0"
authors = ["Your Name <your.email@example.com>"]
edition = "2018"

[dependencies]
# Add your dependencies here

[package.metadata.deb]
maintainer = "Your Name <your.email@example.com>"
description = "A simple CLI application written in Rust"
homepage = "https://github.com/yourusername/my_cli_app"
license-file = "LICENSE"
assets = [
    ["target/release/my_cli_app", "usr/bin/"]
]
```

## Step 4: Build the Debian Package

Use `cargo-deb` to build the `.deb` package.

```bash
cargo deb
```

This will generate a `.deb` file in the `target/debian` directory.

## Step 5: Test the Package

Install the package on your system to ensure it works correctly.

```bash
sudo dpkg -i target/debian/my_cli_app_0.1.0_amd64.deb
```

## Step 6: Distribute the Package

You can distribute the `.deb` package directly to users or upload it to a PPA (for Ubuntu) or a custom repository.

## Step 7: Publishing to a PPA (Ubuntu)

To publish to a PPA, you need a Launchpad account. Follow these steps:

1. **Create a PPA on Launchpad**:

   - Go to [Launchpad](https://launchpad.net/) and create an account if you don't have one.
   - Create a new PPA by following the instructions on the website.

2. **Install `dput`**:

   ```bash
   sudo apt-get install dput
   ```

3. **Generate Source Package**:
   Create a directory structure for the source package:

   ```bash
   mkdir -p ~/my_cli_app-0.1.0
   cp -r target/debian/* ~/my_cli_app-0.1.0
   cd ~/my_cli_app-0.1.0
   ```

4. **Generate Source Files**:

   ```bash
   debuild -S -sa
   ```

5. **Upload to PPA**:
   ```bash
   dput ppa:yourusername/yourppa ../my_cli_app_0.1.0_source.changes
   ```

## Step 8: Creating a Repository for Debian

To create a custom repository for Debian, follow these steps:

1. **Install `reprepro`**:

   ```bash
   sudo apt-get install reprepro
   ```

2. **Set Up Repository Structure**:

   ```bash
   mkdir -p ~/my_repo/{conf,incoming,db,dists,pool}
   cd ~/my_repo
   ```

3. **Create `conf/distributions` File**:

   ```plaintext
   Origin: YourName
   Label: YourRepo
   Suite: stable
   Codename: buster
   Architectures: amd64 source
   Components: main
   Description: My custom repository
   SignWith: yes
   ```

4. **Add Package to Repository**:

   ```bash
   reprepro -b . includedeb buster /path/to/my_cli_app_0.1.0_amd64.deb
   ```

5. **Serve Repository via HTTP**:
   Use a web server like Apache or Nginx to serve the repository.

## Example Directory Structure

Your project directory should look like this:

```
my_cli_app/
├── src/
│   └── main.rs
├── Cargo.toml
├── Cargo.lock
├── target/
│   └── release/
│       └── my_cli_app
└── debian/
    ├── control
    ├── rules
    └── other_debian_files
```

## Downloadable Example

Here's the PKGBUILD content for download:

```plaintext
[package]
name = "my_cli_app"
version = "0.1.0"
authors = ["Your Name <your.email@example.com>"]
edition = "2018"

[dependencies]
# Add your dependencies here

[package.metadata.deb]
maintainer = "Your Name <your.email@example.com>"
description = "A simple CLI application written in Rust"
homepage = "https://github.com/yourusername/my_cli_app"
license-file = "LICENSE"
assets = [
    ["target/release/my_cli_app", "usr/bin/"]
]
```

---

debian helper
lintian
necessary files to publish a debian package
