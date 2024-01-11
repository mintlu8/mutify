# Mutify

[![Crates.io](https://img.shields.io/crates/v/mutify.svg)](https://crates.io/crates/mutify)
[![Docs](https://docs.rs/mutify/badge.svg)](https://docs.rs/mutify/latest/mutify/)

Macro for coercing a `mut var: T` or `var: &mut T` into a `&mut T`.

## Why

A naive apporach would be putting a `&mut` before the expression,
however this doesn't work.

```rust
let func = |v: &mut i32| *v += 1;
let mut b = 0;
let a = &mut b;
// `a` is not mutable.
func(&mut a);
```

## Example

```rust
fn plus_one(n: &mut i32) {
    *n += 1;
}

let mut a = 3;
plus_one(mutify!(a));
assert_eq!(a, 4);

let b = &mut a;
plus_one(mutify!(b));
assert_eq!(a, 5);
```

## Note

A magic function called `__coerce_mut` is used here, don't name your
functions that and you are good!
