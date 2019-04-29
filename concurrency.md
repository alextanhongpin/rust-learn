## Thread
```rust
use std::thread;
use std::time::Duration;

fn main(){
    let handle = thread::spawn(||{
        for i in 1..10 {
            println!("hi number {} from the spawned thread!", i);
            thread::sleep(Duration::from_millis(1));
        }
    });

    // This will wait for the spawned thread to complete before calling the main thread.
    handle.join().unwrap();
    for i in 1..5 {
        println!("hi number {} from the main thread!", i);
        thread::sleep(Duration::from_millis(1));
    }
    // handle.join().unwrap();
}
```


## Closures

```rust
use std::thread;

fn main() {
    let v = vec![1,2,3];
    let handle = thread::spawn(move||{
        println!("here's a vector: {:?}", v);
    });
    handle.join().unwrap();
}
```

## Channels

```rust
use std::sync::mpsc;
use std::thread;

fn main() {
    let (tx, rx) = mpsc::channel();
    thread::spawn(move||{
        let val = String::from("hello");
        tx.send(val).unwrap();
    });
    // This is blocking - hence there is no need to join the handle.
    let received = rx.recv().unwrap();
    println!("got {}", received);
}
```

## Multi-producer

```rust
use std::sync::mpsc;
use std::thread;
use std::time::Duration;

fn main() {
    let (tx, rx) = mpsc::channel();
    thread::spawn(move||{
        let vals = vec![
            String::from("hi"),
            String::from("from"),
            String::from("the"),
            String::from("thread"),
        ];
        for val in vals {
            tx.send(val).unwrap();
            thread::sleep(Duration::from_secs(1))
        }
    });
    for received in rx {
        println!("got {}", received);
    }
}
```

```rust
use std::sync::mpsc;
use std::thread;
use std::time::Duration;

fn main() {
    let (tx, rx) = mpsc::channel();
    let tx1 = mpsc::Sender::clone(&tx);
    thread::spawn(move||{
        let vals = vec![
            String::from("hi"),
            String::from("from"),
            String::from("the"),
            String::from("thread"),
        ];
        for val in vals {
            tx1.send(val).unwrap();
            thread::sleep(Duration::from_secs(1));
        }
    });

    thread::spawn(move||{
        let vals = vec![
            String::from("more"),
            String::from("message"),
            String::from("for"),
            String::from("you"),
        ];
        for val in vals {
            tx.send(val).unwrap();
            thread::sleep(Duration::from_secs(1));
        }
    });

    for received in rx {
        println!("got: {}", received);
    }
}
```

## Mutex

```rust
use std::sync::Mutex;

fn main() {
    let m = Mutex::new(5);
    {
        let mut num = m.lock().unwrap();
        *num = 6
    }
    println!("m is {:?}", m);
}
```

## Atomic reference counter

```rust
use std::sync::{Arc, Mutex};
use std::thread;

fn main() {
    let counter = Arc::new(Mutex::new(0));
    let mut handles = vec![];

    for _ in 0..10 {
        let counter = Arc::clone(&counter);
        let handle = thread::spawn(move || {
            let mut num = counter.lock().unwrap();
            *num += 1;
        };

        handles.push(handle);
    }
    for handle in handles {
        handle.join().unwrap();
    }
    println!("result is {:?}", *counter.lock().unwrap());
}
```

## Moving Data

```rs
use std::thread;
use std::sync::mpsc::{channel, Sender, Receiver};

fn main() {
    const N: i32 = 10;
    let (tx, rx): (Sender<i32>, Receiver<i32>) = channel();
    let handles = (0..N).map(|i| {
        let _tx = tx.clone();
        thread::spawn(move|| {
            let _ = _tx.send(i).unwrap();
        })
    });
    for h in handles {
        h.join().unwrap();
    }
    let numbers: Vec<i32> = (0..N).map(|_|{
        rx.recv().unwrap()
    }).collect();
    println!("{:?}", numbers);
}
```


## Sharing Data
```rs
use std::thread;
use std::sync::{Mutex, Arc};

fn main() {

    let v = Arc::new(Mutex::new(vec![]));
    let handles = (0..10).map(|i| {
        let vector = Arc::clone(&v);
        thread::spawn(move|| {
            let mut v = vector.lock().unwrap();
            (*v).push(i);
        })
    });
    for h in handles {
        h.join().unwrap();
    }
    let values = (*v).lock().unwrap();
    println!("{:?}", values);
}
```
