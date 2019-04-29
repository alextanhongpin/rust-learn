## Setup test for bin project

```rs
fn main() {
    println!("Hello, world!");
}

fn sum(a: i8, b: i8) -> i8 {
    a + b
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_sum() {
        assert_eq!(sum(1, 10), 11);
    }
}
```
