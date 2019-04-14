Error handling with rust with the `?` operator:

-  this can only be used in a function that returns `Result`.

```rust
fn main() {
    let res = hello();
    match res {
        Ok(v) => println!("got value: {}", v),
        Err(e) => println!("got error: {:?}", e)
    }
}

fn m () -> Result<i8, &'static str> {
    Err("bad method")
}

fn hello() -> Result<i8, &'static str> {
    let v = m()?;
    println!("{}", v);
    Ok(v)
}
```
