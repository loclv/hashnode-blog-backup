# Getting started with rust language from JavaScript  knowledge

I have no experience with Rust language at all. So when I try Rust, maybe something I don't understand at the moment I write this. But I want to give it a try!

## Preferences

* [https://www.rust-lang.org/learn/get-started](https://www.rust-lang.org/learn/get-started)
    

## 🌱 Getting started

After installing Rush language based on your using OS. To verify the successful installation:

```bash
rustc --version
# output: rustc 1.67.0 (fc594f156 2023-01-24)
cargo --version
# output: cargo 1.67.0 (8ecd4f20a 2023-01-10)
```

## 🍏 **Generating a new project**

```bash
cargo new hello-rust
cd hello-rust
ls
code .
```

Next, we need to prepare the development environment. For VSCode, I'm using [Rust analyzer](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer) extension. Other extensions:

* [even-better-toml](https://marketplace.visualstudio.com/items?itemName=tamasfe.even-better-toml) - Syntax highlighting and validation for TOML documents (`Cargo.toml`)
    

```bash
cargo run
```

Output:

* Compiling - hello-rust v0.1.0 (path\\to\\hello-rust)
    
* Finished - dev \[unoptimized + debuginfo\] target(s) in 0.71s
    
* Running - `target\debug\hello-rust.exe`
    

```bash
cargo build
```

Output:

* Finished dev \[unoptimized + debuginfo\] target(s) in 0.00s
    

```bash
cargo test
```

Output:

* Compiling hello-rust v0.1.0 (path\\to\\hello-rust)
    
* Finished test \[unoptimized + debuginfo\] target(s) in 0.32s
    
* Running unittests src\\main.rs (target\\debug\\deps\\hello\_rust-e2e48f3e969733ad.exe)
    

## 🌽 Source code

`Cargo.toml`:

```toml
[package]
name = "hello-rust"
version = "0.1.0"
edition = "2021"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
```

`Cargo.lock` :

```toml
# This file is automatically @generated by Cargo.
# It is not intended for manual editing.
version = 3

[[package]]
name = "hello-rust"
version = "0.1.0"
```

`.gitignore` :

```ini
/target
```

`src\main.rs` :

```rust
fn main() {
    println!("Hello, world!");
}
```

Let's view deeper in ignored folder:

```bash
tree .
```

My running OS is Windows, so the output is:

```plaintext
PATH\TO\HELLO-RUST
├───src
└───target
    └───debug
        ├───.fingerprint
        │   ├───hello-rust-56ddd413b0849874
        │   ├───hello-rust-5820db0b29385df2
        │   ├───hello-rust-71cc4f1d00a50391
        │   └───hello-rust-e2e48f3e969733ad
        ├───build
        ├───deps
        ├───examples
        └───incremental
            ├───hello_rust-13xvhef7ifhwo
            │   └───s-gi0ldsfjao-e7nyh-1a9bmzoyjcn30
            ├───hello_rust-2mpimy89ql4lt
            │   └───s-gi0ldsfj7a-rw39ce-2a18ew5zcrcaz
            ├───hello_rust-3e9t63lxisjk4
            │   └───s-gi0lv1s4s4-14t6l41-9wekp6y89fms
            └───hello_rust-p3ci3gxgh4dj
                └───s-gi0lvjh8bc-sqyxds-3eqvyiv620wj4
```

The main folder structure:

```plaintext
├── Cargo.toml
└── src
    └── main.rs
```

## 🍍 Compared categories

Here are the JS equivalents:

| category | Rust | JS | difference |
| --- | --- | --- | --- |
| Package manager | cargo | `npm`, `pnpm`, `yarn` | cargo is also a build tool |
| Package manager file configuration | Cargo.toml | package.json | cargo is using the TOML format |
| Package library dependencies | `[dependencies]` | `"dependencies"` | ? |
| Package library dependencies for development | `[dev-dependencies]`, `[build-dependencies]` | `"devDependencies"` | With `npm`, other option is `peerDependencies`, `peerDependenciesMeta`, `bundleDependencies`, `optionalDependencies` |
| community’s crate registry | [crates.io](http://crates.io) | [npmjs.com](http://npmjs.com) | ? |
| Add dependencies | `cargo add` | `yarn add` | ? |
| Remove dependencies | `cargo remove` | `yarn remove` | ? |
| run your project with | `cargo run` | `pnpm start` | `cargo` used compiler - `rustc` and execute the compiled file |
| compiling script | `cargo build` | none | JavaScript is an interpreted language, not a compiled language |
| coding convention | tab size is 4 spaces | tab size is 2 spaces |  |
| function syntax keyword | `fn` | `function` |  |
| ... | ... | ... | ... |

I think I need to rest now, too many things to learn!