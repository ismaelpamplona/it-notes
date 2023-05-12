# Big O

Big O is a notation used to describe the computational complexity of an algorithm. The computational complexity of an algorithm is split into two parts: time complexity and space complexity. 

**The time complexity** of an algorithm is the amount of time the algorithm needs to run relative to the input size. 

**The space complexity** of an algorithm is the amount of memory allocated by the algorithm when run relative to the input size.

Complexity is described by a function of variables that can change with the input. Examples:

$
O(n) \\
O(n²) \\
O(2^n) \\
O(logn) \\
O(n⋅m)
$

These functions describe how the amount of operations/memory needed by the algorithm grows as the arguments tend to infinity. Because the variables are tending to infinity, **CONSTANTS ARE ALWAYS IGNORED**. That means that: 

$$
O(9999999n) = O(8n) = O(n) = O(^n/_{500}) \\
O(2^n + n² - 500n) = O(2^n)
$$

## Analyzing time complexity

```Rust
// Given an array "arr" with length n
for n in &arr {
    println!("{n}")
}
```
In each for loop iteration, we are performing a print, which costs $O(1)$. For n iterations: $O(n)$.


```Rust
// Given an array "arr" with length n
for n in &arr {
    for i in 0..500_000 {
        println!("{n}");
    }
}
```
In each inner for loop iteration iterates 500k times, which means each outer for loop iteration costs $O(500000) = O(1)$. So, The outer for loop iterates $n$ times, which gives a time complexity of $O(n)$.


```Rust
// Given an array "arr" with length n
for n in &arr {
    for m in &arr {
        println!("{n}")
    }
}
```
In each inner for loop iteration, we are performing a print, which cost $O(1)$ and runs $n$ times. So, The outer for loop iterates $n$ times, which gives a time complexity of $O(n⋅n) = O(n²)$.


```Rust
// Given an array "arr" with length n
// Given an array "arr2" with length m
for n in &arr {
    println!("{n}")
}

for n in &arr {
    println!("{n}")
}

for n in &arr2 {
    println!("{n}")
}
```
This algorithm has a time complexity of $O(n+m)$. The first two both cost O(n), and the third one costs $O(m)$. This gives a time complexity of $O(2n + m) = O(n + m)$


```Rust
// Given an array "arr" with length n
    for i in 0..arr.len() {
        for j in i..arr.len() {
            println!("{}", arr[i] + arr[j]);
        }
    }

```
The inner for loop is dependent on what iteration the outer for loop is currently on. The first time the inner for loop is run, it runs 
$n$ times. The second time $n-1$ times, then $n-2$, $n-3$, and so on.

That means that ${[n⋅(n+1)]}/2 = {(n² + n)} / 2$

## Analyzing space complexity

```Rust
// Given an array "arr" with length n
for num in &arr {
    println!("{num}")
}
```
This algorithm has a space complexity of $O(1)$. The only space allocated is an integer variable `num`, which is constant relative to 
$n$.


```Rust
// Given an array "arr" with length n
let mut doubled_vec: Vec<i32> = vec![];
for num in arr {
    doubled_vec.push(num*2);
}
```
This algorithm has a space complexity of $O(n)$. For each iteration, we push a new value to the `doubled_vec` variable. The vector `doubled_vec` stores $n$ integers at the end of the algorithm.


```Rust
// Given an array "arr" with length n
let arr: Vec<i32> = (0..500).collect();
let mut nums = vec![];
let one_hundredth = arr.len() / 100;
for i in 0..one_hundredth {
    nums.push(arr[i]);
}
```
The array nums stores the first 1% of numbers in arr. This gives a space complexity of $O(n/100) = O(n)$.


```Rust
// Given an array "arr" with length n,
// Given an array "arr2" with length m,
let arr: Vec<i32> = (1..=10).collect();
let arr2: Vec<i32> = (1..=10).collect();
let mut grid = vec![vec![0; arr2.len()]; arr.len()];
for i in 0..arr.len() {
    for j in 0..arr2.len() {
        grid[i][j] = arr[i] * arr2[j];
    }
}
```
This algorithm has a space complexity of $O(n⋅m)$. We are creating a grid that has dimensions $n⋅m$.