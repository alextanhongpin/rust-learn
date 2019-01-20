## Basic
```rust
#[derive(Debug)]
enum Keyboard {
    Up, Down, Left, Right(i32)
}

fn main() {
    println!("{:?}", Keyboard::Up);
    let right = Keyboard::Right(10);
    let left = Keyboard::Left;
    println!("{:?}", right);
    if let Keyboard::Right(n) = right {
        println!("{}", n);
    }
    
    match right {
        Keyboard::Right(n) => println!("got {}", n),
        _ => println!("none")
    }
    match left {
        Keyboard::Right(n) => println!("got {}", n),
        _ => println!("none")
    }
}
```

Output:

```
Up
Right(10)
10
got 10
none
```
