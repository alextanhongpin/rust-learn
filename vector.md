## Creating a vector from range

```rust
// To convert a range into vector, you need to `.collect()` it and specify the type of the vector.
let nums: Vec<i8> = (1..10).collect();
```

## filter, take and collect

```rust
// This is better.
let numbers: Vec<i8> = (1..)
    .filter(|i| i % 2 == 0)
    .map(|i| i * 3)
    .take(5)
    .collect();

for n in numbers.iter() {
    println!("alternative {}", n);
}

println!("{:?}", numbers);
```

## Mutating values in a vector

```rust
let mut others: Vec<i8> = (1..).filter(|i| i & 2 == 0).take(5).collect();
println!("values {:?}", others);
for i in others.iter_mut() {
    *i += 10;
}
println!("values {:?}", others);
```

## Iterate over values 

```rust
let nums: Vec<i8> = (1..10).collect();

// Iterate over values rather than reference.
let permanent: Vec<i8> = nums.into_iter().filter(|&i| i % 2 == 0).collect();
println!("permanent: {:?}", permanent);
```

## Mutating existing Vector

```rust
fn main() {
    let mut nums: Vec<i8> = (1..10).collect();
    {
        let numbers = &mut nums[2..4];
        println!("numbers is {:?}", numbers);
        for i in numbers.iter_mut() {
            *i += 10;
        }
        println!("{:?}", numbers);
    }
    println!("{:?}", nums);
}
// numbers is [3, 4]
// [13, 14]
// [1, 2, 13, 14, 5, 6, 7, 8, 9]
```
