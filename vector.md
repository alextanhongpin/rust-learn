# Vector 

- is allocated on the heap
- can grow or shrink in size
- all elements must be of the same type


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

## Modifying vectors

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
    
    {
        let numbers = &mut nums.iter_mut().filter(|ref i| ***i % 2 == 0).collect::<Vec<_>>();
        println!("numbers is {:?}", numbers);
        println!("first is {:?}", numbers[0]);
        *numbers[0] *= 30;
        for ref mut i in numbers.iter_mut() {
            ***i += 22;
        }
        println!("updated numbers is {:?}", numbers);
    }
    println!("{:?}", nums);
}
// numbers is [3, 4]
// [13, 14]
// numbers is [2, 14, 6, 8]
// first is 2
// updated numbers is [82, 36, 28, 30]
// [1, 82, 13, 36, 5, 28, 7, 30, 9]
```

## Basic 

Vector can be constructed from iterators through the `.collect()` method. Example with `range`:
```rust
fn main() {
    let nums: Vec<i32> = (0..7).collect();
    println!("{:?}", nums);
    
    // Without .iter(), the numbers will be moved, and the println! below will
    // not work.
    for n in nums.iter() {
        print!("{} ", n);
    }
    println!("{:?}", nums);
    
    let mut nums: Vec<i32> = (0..5).collect();
    let n = nums.pop().unwrap();
    println!("{}", n);
    println!("{:?}", nums);
    
    nums.push(10);
    println!("{:?}", nums);
    
    // Mutating the vectors.
    for n in nums.iter_mut() {
        *n += 10;
    }
    println!("{:?}", nums);
}
```

Output:
```
[0, 1, 2, 3, 4, 5, 6]
0 1 2 3 4 5 6 [0, 1, 2, 3, 4, 5, 6]
4
[0, 1, 2, 3]
[0, 1, 2, 3, 10]
[10, 11, 12, 13, 20]
```

## Map, filter
```
fn main() {
 let nums: Vec<i32> = (1..100).collect();
 let total = nums.iter().fold(0, |sum, i| sum + i);
 println!("{:?}", total);
 
 let min = nums.iter().min();
 println!("{:?}", min);
 
 let max = nums.iter().max();
 println!("{:?}", max);
 
 // clone().into_iter()
 let count = nums.iter().count();
 println!("{:?}", count);
 
 let even = nums.iter().filter(|&i| i % 2 == 0).collect::<Vec<_>>();
 println!("{:?}", even.len());
 println!("{:?}", &even[..5]);
 println!("{:?}", nums.len());
}
```

Output:

```
4950
Some(1)
Some(99)
99
49
[2, 4, 6, 8, 10]
99
```
