# Base62 implementation in rust

```rust
const BASE62: u64 = 62; 
static BASE62_CHARS: &'static str = "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";

fn main() {
    println!("max u64: {:?}", u64::max_value());
    println!("encode base62: {:?}", encode(280));
    println!("decode base62: {:?}", decode(String::from("Evil")));
}
fn encode(i: u64) -> String {
    // Create a new string. Similar to strings.Builder in golang. 
    let mut str = String::new();
    // Make a mutable index.
    let mut i = i;
    loop {
        // Convert the string into characters to get the char at the nth index.
        // nth() only accepts usize - convert the i64 to usize. Unwrap the 
        // result.
        let c = BASE62_CHARS.chars().nth((i % BASE62) as usize).unwrap();
        // This is an O(n) operation. Push to front.
        str.insert(0, c);
        i = i / BASE62;
        if i == 0 {
            break;
        };
    };
    return str;
}

fn decode(s: String) -> u64 {
    let mut i = 0_u64;
    for c in s.chars() {
        // Find the index of the character in string.
        i = i * BASE62 + (BASE62_CHARS.find(c).unwrap() as u64);
    }
    return i;
}
```
