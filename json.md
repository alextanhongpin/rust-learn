```rust
use rustc_serialize::json::{self};

fn main() {
    let svc = Service::new(9);
    println!("{}", svc.get());
    println!("{}", svc.get());
    println!("{:?}", json::encode(&Some(42)));
    let encoded = json::encode(&svc);
    println!("{:?}", encoded);
    let jsonstr = encoded.unwrap();
    let decoded: Result<Service,_> = json::decode(&jsonstr);
    println!("{:?}", decoded);    
}

#[derive(Debug, RustcDecodable, RustcEncodable)]
struct Service {
    value: i8
}

impl Service {
    fn new(value: i8)-> Self {
        Service{value}
    }
    fn get(&self) -> i8 {
        self.value * 10
    }
}
```
