```rust
trait Countable {
    fn count(&self, ch: char) -> i8;
}

impl Countable for str {
    fn count(&self, ch: char) -> i8 {
        self.chars().filter(|c| *c == ch).count() as i8
    }
}

fn main() {
    let count = "hello".count('l');
    println!("{:?}", count);
}
```
