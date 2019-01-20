```rust
trait Countable {
    fn count(&self, ch: char) -> i8;
}

impl Countable for str {
    fn count(&self, ch: char) -> i8 {
        self.chars().map(|c| match c == ch {
            true => 1,
            _ => 0
        }
        ).fold(0, |sum, i| sum + i)
    }
}

fn main() {
    let count = "hello".count('l');
    println!("{:?}", count);
}
```
