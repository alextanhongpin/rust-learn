## Multiple Owners

Expensive:

```rs
#[derive(Debug)]
struct FileName {
    name: String,
    ext: String
}

fn main() {
    let name = String::from("main");
    let ext = String::from("rs");
    
    for _ in 0..3 {
        println!("{:?}", FileName{
            name: name.clone(),
            ext: ext.clone()
        })
    }
}
```

Better:

```rs
use std::rc::Rc;

#[derive(Debug)]
struct FileName {
    name: Rc<String>,
    ext: Rc<String>
}

fn main() {
    let name = Rc::new(String::from("main"));
    let ext = Rc::new(String::from("rs"));
    
    for _ in 0..3 {
        println!("{:?}", FileName{
            name: name.clone(),
            ext: ext.clone()
        })
    }
}
```
