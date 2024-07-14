# Time Complexity and Space Complexity

## Time Complexity

### Introduction

Time complexity is a way to describe the amount of time an algorithm takes to complete as a function of the length of the input. It gives an upper bound on the running time, which helps to understand the worst-case scenario.

### Big O Notation

Big O notation is used to express time complexity. It provides an upper limit on the growth rate of an algorithm's running time.

#### Common Time Complexities

- **$O(1)$**: Constant time
  - The running time does not change with the size of the input.
  - Example: Accessing an element in an array by index.
- **$O(log n)$**: Logarithmic time
  - The running time grows logarithmically with the input size.
  - Example: Binary search in a sorted array.
- **$O(n)$**: Linear time
  - The running time grows linearly with the input size.
  - Example: Iterating through an array.
- **$O(n log n)$**: Linearithmic time
  - The running time grows as the product of linear and logarithmic terms.
  - Example: Efficient sorting algorithms like merge sort and quicksort.
- **$O(n^2)$**: Quadratic time
  - The running time grows quadratically with the input size.
  - Example: Nested loops in a simple sorting algorithm like bubble sort.
- **$O(2^n)$**: Exponential time
  - The running time grows exponentially with the input size.
  - Example: Solving the traveling salesman problem using brute force.
- **$O(n!)$**: Factorial time
  - The running time grows factorially with the input size.
  - Example: Generating all permutations of a set.

#### Examples

1. **$O(1)$ - Constant Time**

   ```javascript
   function getFirstElement(arr) {
     return arr[0];
   }
   ```

2. **$O(n)$ - Linear Time**

   ```javascript
   function printElements(arr) {
     for (let i = 0; i < arr.length; i++) {
       console.log(arr[i]);
     }
   }
   ```

3. **$O(n^2)$ - Quadratic Time**
   ```javascript
   function printPairs(arr) {
     for (let i = 0; i < arr.length; i++) {
       for (let j = 0; j < arr.length; j++) {
         console.log(arr[i], arr[j]);
       }
     }
   }
   ```

## Space Complexity

### Introduction

Space complexity is a measure of the amount of memory an algorithm needs to run as a function of the length of the input. It includes the memory needed for the input, auxiliary variables, and data structures.

### Big O Notation for Space Complexity

Similar to time complexity, space complexity can be expressed using Big O notation.

#### Examples

1. **$O(1)$ - Constant Space**

   ```javascript
   function getFirstElement(arr) {
     return arr[0];
   }
   ```

2. **$O(n)$ - Linear Space**
   ```javascript
   function createArray(n) {
     const arr = [];
     for (let i = 0; i < n; i++) {
       arr.push(i);
     }
     return arr;
   }
   ```

### Trade-offs

There is often a trade-off between time complexity and space complexity. Optimizing for one can lead to increased usage of the other.

### Example Analysis

Let's analyze the time and space complexity of a common algorithm: merge sort.

#### Merge Sort

```javascript
function mergeSort(arr) {
  if (arr.length <= 1) {
    return arr;
  }

  const middle = Math.floor(arr.length / 2);
  const left = arr.slice(0, middle);
  const right = arr.slice(middle);

  return merge(mergeSort(left), mergeSort(right));
}

function merge(left, right) {
  let result = [];
  let leftIndex = 0;
  let rightIndex = 0;

  while (leftIndex < left.length && rightIndex < right.length) {
    if (left[leftIndex] < right[rightIndex]) {
      result.push(left[leftIndex]);
      leftIndex++;
    } else {
      result.push(right[rightIndex]);
      rightIndex++;
    }
  }

  return result.concat(left.slice(leftIndex)).concat(right.slice(rightIndex));
}
```

- **Time Complexity**: O(n log n)
  - The merge sort algorithm divides the array into halves log n times and performs a linear merge operation for each division.
- **Space Complexity**: O(n)
  - The merge function requires additional space proportional to the input size to hold the sorted array.

### Summary

- **Time Complexity**: Measures the time an algorithm takes to complete as a function of input size.
- **Space Complexity**: Measures the amount of memory an algorithm uses as a function of input size.
- **Big O Notation**: Used to describe both time and space complexity.
- **Trade-offs**: Optimizing for time complexity can lead to increased space complexity and vice versa.
