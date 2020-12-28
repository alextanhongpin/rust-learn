Given an array of 10 users (male, female) in random order, print all the females first, then males in a single iteration.

```rust
fn main() {
    let people: Vec<&str> = "M F M F M F M F M F".split(" ").collect();
    let len = people.len();
    for i in 0..(2 * len) {
        match (people[i % len], i >= len)  {
            ("M", true) => println!("male"),
            ("F", false) => println!("female"),
            _ => continue
        }
    }
}
```


## Reverse range

A forward loop is like this:
```rust
for x in 0..100 {
    println!("{}", x);
}
```

And a reverse loop is done by calling Iterator::rev to reverse the order:

```rust
for x in (0..100).rev() {
    println!("{}", x);
}
```
