# Functional Programming Concepts

## Map

The `map` method creates a new array populated with the results of calling a provided function on every element in the calling array.

### Syntax

```javascript
const newArray = array.map(callback(element[, index[, array]])[, thisArg])
```

- **callback:** Function that produces an element of the new Array, taking three arguments:
  - **element:** The current element being processed in the array.
  - **index (optional):** The index of the current element being processed in the array.
  - **array (optional):** The array `map` was called upon.
- **thisArg (optional):** Value to use as `this` when executing the callback.

### Example

```javascript
const numbers = [1, 2, 3, 4];
const doubled = numbers.map((num) => num * 2);
console.log(doubled); // [2, 4, 6, 8]
```

## Filter

The `filter` method creates a new array with all elements that pass the test implemented by the provided function.

### Syntax

```javascript
const newArray = array.filter(callback(element[, index[, array]])[, thisArg])
```

- **callback:** Function is a predicate, to test each element of the array. Return `true` to keep the element, `false` otherwise. It takes three arguments:
  - **element:** The current element being processed in the array.
  - **index (optional):** The index of the current element being processed in the array.
  - **array (optional):** The array `filter` was called upon.
- **thisArg (optional):** Value to use as `this` when executing the callback.

### Example

```javascript
const numbers = [1, 2, 3, 4, 5];
const evenNumbers = numbers.filter((num) => num % 2 === 0);
console.log(evenNumbers); // [2, 4]
```

## Reduce

The `reduce` method executes a reducer function (that you provide) on each element of the array, resulting in a single output value.

### Syntax

```javascript
const result = array.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])
```

- **callback:** Function to execute on each element in the array, taking four arguments:
  - **accumulator:** The accumulator accumulates the callback's return values.
  - **currentValue:** The current element being processed in the array.
  - **index (optional):** The index of the current element being processed in the array.
  - **array (optional):** The array `reduce` was called upon.
- **initialValue (optional):** A value to use as the first argument to the first call of the callback. If no initial value is supplied, the first element in the array will be used as the initial accumulator value and skipped as currentValue.

### Example

```javascript
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((acc, curr) => acc + curr, 0);
console.log(sum); // 10
```

## Combined Example

Here’s an example that combines `map`, `filter`, and `reduce`:

### Example

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

// Step 1: Double the numbers
const doubled = numbers.map((num) => num * 2);

// Step 2: Filter out numbers greater than 5
const filtered = doubled.filter((num) => num > 5);

// Step 3: Sum the remaining numbers
const sum = filtered.reduce((acc, num) => acc + num, 0);

console.log(sum); // 24 (6 + 8 + 10)
```

### Explanation

1. **map:** Doubles each number in the array resulting in `[2, 4, 6, 8, 10, 12]`.
2. **filter:** Keeps only numbers greater than 5 resulting in `[6, 8, 10, 12]`.
3. **reduce:** Sums the numbers resulting in `24`.

### Summary

- **map:** Transforms each element of an array using a provided function and returns a new array.
- **filter:** Filters elements of an array based on a condition and returns a new array.
- **reduce:** Reduces an array to a single value by executing a reducer function on each element.
