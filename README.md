# Calling Rust from C simplest example

1. Create project

```bash
$ cargo new --lib ffi-tutorial
```

2. Edit `Cargo.toml`

```diff
[package]
name = "ffi-tutorial"
version = "0.1.0"
edition = "2021"

+[lib]
+crate-type = ["cdylib"]

[dependencies]
```

> Use `cdylib` to creates dynamic lib.
> To creates static lib, use `staticlib` instead.


3. Edit `src/lib.rs`

```diff
+#![deny(improper_ctypes_definitions)]
+
+use std::os::raw::c_int;
+
+#[no_mangle]
+pub extern "C" fn add(left: c_int, right: c_int) -> c_int {
-pub fn add(left: usize, right: usize) -> usize {
     left + right
 }
 
 #[cfg(test)]
 mod tests {
     use super::*;
 
     #[test]
     fn it_works() {
         let result = add(2, 2);
         assert_eq!(result, 4);
     }
 }
```

4. Build/Generates header with `cbindgen`

```bash
$ cargo install cbindgen
$ touch ffi-tutorial.toml
$ cargo build --release
$ cbindgen --config cbindgen.toml --crate ffi-tutorial --output libffi_tutorial.h --lang c
$ mv libffi_tutorial.h target/release/libffi_tutorial.so main
$ cd main
$ make && ./main
```

5. Call in C Programme


# See also

[A little Rust with your C - The Embedded Rust Book](https://docs.rust-embedded.org/book/interoperability/rust-with-c.html)

[Calling Rust from C - Comprehensive Rust 🦀](https://google.github.io/comprehensive-rust/android/interoperability/with-c/rust.html)