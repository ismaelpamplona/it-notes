
# Publishing a Rust CLI App in AUR

Publishing a Rust CLI app to the Arch User Repository (AUR) involves several steps, from creating the package to submitting it to the AUR. Below is a detailed step-by-step guide.

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
You'll need `base-devel` and `git` packages installed.

```bash
sudo pacman -S base-devel git
```

## Step 3: Create a PKGBUILD File
The PKGBUILD file contains the build instructions for your package.

1. **Navigate to your project directory**:
    ```bash
    cd my_cli_app
    ```

2. **Create the PKGBUILD file**:
    ```bash
    touch PKGBUILD
    ```

3. **Edit the PKGBUILD file** with the following content:

```bash
# Maintainer: Your Name <your.email@example.com>
pkgname=my_cli_app
pkgver=0.1.0
pkgrel=1
pkgdesc="A simple CLI application written in Rust"
arch=('x86_64')
url="https://github.com/yourusername/my_cli_app"
license=('MIT')
depends=('glibc')
makedepends=('rust' 'cargo')
source=("$pkgname-$pkgver.tar.gz::https://github.com/yourusername/my_cli_app/archive/v$pkgver.tar.gz")
sha256sums=('SKIP')

build() {
    cd "$srcdir/$pkgname-$pkgver"
    cargo build --release --locked
}

package() {
    cd "$srcdir/$pkgname-$pkgver"
    install -Dm755 "target/release/$pkgname" "$pkgdir/usr/bin/$pkgname"
}
```

## Step 4: Build the Package
Build the package to ensure everything is set up correctly.

1. **Download the source**:
    ```bash
    makepkg -o
    ```

2. **Build the package**:
    ```bash
    makepkg -si
    ```

3. **Verify the installation**:
    ```bash
    my_cli_app --version
    ```

## Step 5: Create an AUR Account
If you don’t have an AUR account, [create one here](https://aur.archlinux.org/register/).

## Step 6: Submit Your Package to AUR
1. **Initialize a git repository in your project directory**:
    ```bash
    git init
    git remote add aur ssh://aur@aur.archlinux.org/my_cli_app.git
    ```

2. **Add your PKGBUILD file to the repository**:
    ```bash
    git add PKGBUILD
    git commit -m "Initial commit"
    git push -u aur master
    ```

## Step 7: Maintain Your Package
After publishing, ensure you maintain the package by updating the PKGBUILD file and the version numbers whenever there are new releases.

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
└── PKGBUILD
```

## Downloadable PKGBUILD Example

Here's the PKGBUILD content for download:

```plaintext
# Maintainer: Your Name <your.email@example.com>
pkgname=my_cli_app
pkgver=0.1.0
pkgrel=1
pkgdesc="A simple CLI application written in Rust"
arch=('x86_64')
url="https://github.com/yourusername/my_cli_app"
license=('MIT')
depends=('glibc')
makedepends=('rust' 'cargo')
source=("$pkgname-$pkgver.tar.gz::https://github.com/yourusername/my_cli_app/archive/v$pkgver.tar.gz")
sha256sums=('SKIP')

build() {
    cd "$srcdir/$pkgname-$pkgver"
    cargo build --release --locked
}

package() {
    cd "$srcdir/$pkgname-$pkgver"
    install -Dm755 "target/release/$pkgname" "$pkgdir/usr/bin/$pkgname"
}
```
