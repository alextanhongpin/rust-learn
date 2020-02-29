# rust-learn
Stuff I learn about Rust


## Modules

To export modules, create a `mod.rs` in the folder you want export the methods/variables. They must be public `pub` in order to be exported:
```
src/
  main.rs
  hello/
    hello.rs
    mod.rs
```

In `src/hello/hello.rs`:
```rust
pub fn hello() {
  print!("hello world")
}
```

In `src/hello/mod.rs`:
```
// Make the module hello (based on filename hello.rs) public.
pub mod hello;
```

In `main.rs`:

```rust
// Import the module hello.
mod hello;
```


## Rust 2018 file structure
`main.rs`:

```rs
mod greet;

fn main() {
    greet::hello();
    greet::scream::exec();
}
```

`greet.rs`:
```rs
pub mod salutation;
pub mod scream;

pub fn hello() {
    println!("hello world!");
}
```

`greet/scream.rs`:
```rs
// Super refers to relative to this folder.
use super::salutation;

pub fn exec() {
    println!("screaming!");
    salutation::salute();
    // Create is relative to project.
    // crate::greet::salutation::salute();
}
```

`greet/salutation.rs`:

```rs
pub fn salute() {
    println!("hello!");
}
```
