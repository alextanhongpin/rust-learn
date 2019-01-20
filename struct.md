```rust
// Make the struct printable.
#[derive(Debug)]
struct A {
    a: i32,
    b: String,
    c: bool
}

fn main() {
    let a = A{
        a: 10,
        b: "john".to_string(),
        c: false
    };
    println!("{:?}", a);
    
    let b = A{
        // ..a // Must be at the bottom
        c: true,
        ..a
    };
    println!("{:?}", b);
}
```
