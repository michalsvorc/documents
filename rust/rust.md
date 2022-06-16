# Rust

- [The Rust Programming Language Book](https://doc.rust-lang.org/book/title-page.html)
- [Rust Playground](https://play.rust-lang.org)

## Macro vs Function

- [Macro - Documentation](https://doc.rust-lang.org/book/ch19-06-macros.html)

Using a `!` means that you’re calling a macro instead of a normal function.

```rust
println!("Hello, world!");
```

## Variables

[Documentation](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html)

`let` variables can be redeclared when using original value:

```rust
let x = 5
let x = 5 + 1
```

Variables can be shadowed.

## Data types

- [Documentation](https://doc.rust-lang.org/book/ch03-02-data-types.html)

### Integers

- [Documentation](https://doc.rust-lang.org/book/ch03-02-data-types.html#integer-types)

How do you know which type of integer to use? If you’re unsure, Rust’s defaults are generally good choices, and integer
types default to `i32`: this type is generally the fastest, even on 64-bit systems. The primary situation in which you’d
use `isize` or `usize` is when indexing some sort of collection.
