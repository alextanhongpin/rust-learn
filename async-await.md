
## Async/Await
```rust
use futures::executor::block_on;

async fn do_something() {
    println!("hello world");
}

fn main() {
    block_on(do_something());
}
```
## Multiple async

```rust
use futures::executor::block_on;

async fn learn_song() -> String {
    "This is a love song".to_string()
}

async fn sing_song(song: String) {
    println!("learning song {}", song);
}

async fn dance() {
    println!("dancing");
}

async fn learn_and_sing() {
    let song = learn_song().await;
    sing_song(song).await;
}

async fn async_main() {
    let f1 = learn_and_sing();
    let f2 = dance();
    
    futures::join!(f1, f2);
}

fn main() {
    block_on(async_main());
}
```

## Futures
```rust
use core::future::Future;
use futures::executor::block_on;

async fn foo() -> u8 { 8 }

fn bar() -> impl Future<Output = u8> {
    async {
        let x: u8 = foo().await;
        x + 5
    }
}

fn main() {
    println!("got: {}", block_on(bar()));
}
```
