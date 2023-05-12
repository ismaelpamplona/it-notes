# Recursion

## YouTube Videos:

[How to write Recursive Functions](https://www.youtube.com/watch?v=ggk7HbcnLG8)

[Recursion - Part 7 of Functional Programming in JavaScript - FunFunFunction](https://www.youtube.com/watch?v=k7-N8R0-KY4)

[Recursion in software development - freeCodeCamp.org](https://www.youtube.com/watch?v=vPEJSJMg4jY)

[[BONUS] Debugging recursive functions—CMPUT 175 - CMPUT 175](https://www.youtube.com/watch?v=Btoobiaf5Gw)

## Idea

1. Divide the problem into smaller sub-problems.
2. Specify the base condition to stop the recursion.

## Basic Structure of a Recursion Function

1. Specify the **recursive procedure**
2. Specify your **base case**

```Rust
 fn fact() {
     if () { 
         // base case (2)
     } else { 
         // recursive procedure (1)
     }
 }
``` 

## Calculate the factorial of a number

### 1. Divide the problem into smaller sub-problems:
```
fact(1) = 1
fact(2) = 1 * 2 = 2 => 2 * fact(1)
fact(3) = 1 * 2 * 3 = 6 => 3 * fact(2)
fact(4) = 1 * 2 * 3 * 4 = 24 => 4 * fact(3)

...

fact(n) = n * fact(n - 1)
```

### 2. Specify the base condition to stop recursion:

- Base condition is the one which doesn't require to call the same function again and it helps in stopping the recursion. 
- The `fact(1) = 1` is the unique line that we do not call the recursion.
  
#### Rust
```Rust
fn fact(n: i32) -> i32 {
  if n < 2 { 
      1
  } else { 
      n * fact(n - 1)
  }
}
``` 
#### Javascript
```JavaScript
let factorial = (n) => {

  if (n<1) return 1;
  let prev =  factorial(n-1);
  return n*prev

}

console.log(factorial(3));
```

```JavaScript
let categories = [
  {id: "animals", "parent": null},
  {id: "mammals", "parent": "animals"},
  {id: "cats", "parent": "mammals"},
  {id: "dogs", "parent": "mammals"},
  {id: "chihuahua", "parent": "dogs"},
  {id: "labrador", "parent": "dogs"},
  {id: "persian", "parent": "cats"},
  {id: "siamese", "parent": "cats"}
];

// console.log(categories);

const makeTree = (categories, parent) => {
  let node = {};
  categories
    .filter(c => c.parent === parent)
    .forEach(c => node[c.id] = makeTree(categories, c.id));

 return node;
}

const show = (data) => {
  console.log(JSON.stringify(data, null, 2));
}

show(makeTree(categories, null))
```

## Recursion X Iterative

### Iterative
```Rust
let arr: Vec<i32> = (1..=3).collect();
fn print_num(arr: Vec<i32>) {
    for el in arr {
        println!("{el}");
    }
}

print_num(arr);
// 1
// 2
// 3
```

### Recursion
```Rust
fn print_num(num: i32) {
    println!("{num}");
    if num < 3 {
        print_num(num + 1);
    }
    println!("End of call where num = {num}")
}

print_num(1);
// 1
// 2
// 3
// End of call where num = 3
// End of call where num = 2
// End of call where num = 1
```

## Fibonacci

The Fibonacci numbers are a sequence of numbers starting with 0, 1. Then, each number is defined as the sum of the previous two numbers. The first few Fibonacci numbers are 0, 1, 1, 2, 3, 5, 8. 

$$
F_n = F_{n-1} + F_{n-2}
$$

```Rust
fn return_nth_fibo_number(n: i32) -> i32 {
    if n <= 1 {
        // base case
        return n;
    } else {
        let one_back = return_nth_fibo_number(n - 1);
        let two_back = return_nth_fibo_number(n - 2);
        return one_back + two_back;
    }
}

println!("{}", return_nth_fibo_number(0)); // 0
println!("{}", return_nth_fibo_number(1)); // 1
println!("{}", return_nth_fibo_number(2)); // 1
println!("{}", return_nth_fibo_number(3)); // 2
println!("{}", return_nth_fibo_number(4)); // 3
println!("{}", return_nth_fibo_number(5)); // 5
println!("{}", return_nth_fibo_number(6)); // 8
println!("{}", return_nth_fibo_number(8)); // 21
println!("{}", return_nth_fibo_number(9)); // 34
```
