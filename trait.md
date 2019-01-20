## Sample trait
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

## Standard Trait

```rust
struct Magician {
    name: &'static str
}

impl std::fmt::Display for Magician {
    fn fmt(&self, f: &mut std::fmt::Formatter) -> std::fmt::Result {
        write!(f, "{} the magician", self.name)
    }
}
fn main() {
    let m = Magician{
        name: "Merlin"
    };
    println!("{}", m);
}
```
