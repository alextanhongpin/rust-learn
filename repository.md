## Repository Pattern with Rust

```rust
use std::collections::HashMap;

#[derive(Debug)]
struct User {
    id: &'static str,
    name: &'static str,
    age: i32,
}

impl User {
    fn new(id: &'static str, name: &'static str, age: i32) -> Self {
        User { id, name, age }
    }
}

trait Repository<'a> {
    fn get(&mut self, id: &'a str) -> Result<&User, &'a str>;
    fn save(&mut self, user: User) -> Result<bool, &'a str>;
}

struct InMemory<'s> {
    users: HashMap<&'s str, User>,
}

impl InMemory<'_> {
    fn new() -> Self {
        InMemory {
            users: HashMap::new(),
        }
    }
}

impl<'a, 's> Repository<'a> for InMemory<'s> {
    fn get(&mut self, id: &'a str) -> Result<&User, &'a str> {
        match self.users.get(id) {
            Some(user) => Ok(user),
            None => Err("user does not exists"),
        }
    }
    fn save(&mut self, user: User) -> Result<bool, &'a str> {
        self.users.insert(user.id, user);
        Ok(true)
    }
}

fn main() {
    let john = User::new("1", "john", 20);
    let mut memory = InMemory::new();
    println!("saved: {:?}", memory.save(john));
    println!("query: {:?}", memory.get("1"));
}
```
