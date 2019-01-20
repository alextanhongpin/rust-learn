```rust
fn main() {
    // String.
    let name: String = "john doe".to_string();
    println!("name: {}", name);
    
    // String slice.
    let person: &str = "john doe";
    println!("person: {}", person);
    
    get_len(&name);
    get_len(person);
    
    // To string allocates heap memory, & does not.
    println!("{}", person.to_string() == name);
    println!("{}", person == name);
    println!("{}", person == &name);
    
    // Basic looping for characters.
    for c in name.chars() {
        println!("char is {}", c);
    }
    
    for word in name.split(" ") {
        println!("word is {}", word);
    }
    // This code allocates a new memory for the modified string.
    let new_name = name.replace("john", "jane");
    println!("{}", new_name);
    println!("{}", name);
}

// Passing a String as an argument allocates memory, hence it is better to pass 
// in string slice.
fn get_len(s: &str) {
    println!("{:?}", s.len());
}
```

Output:
```
name: john doe
person: john doe
8
8
true
true
true
char is j
char is o
char is h
char is n
char is  
char is d
char is o
char is e
word is john
word is doe
jane doe
john doe
```
