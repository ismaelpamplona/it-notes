# Arrays, Objects, and Maps/Sets in JavaScript

## Arrays

### Introduction

An array is an ordered collection of items that can be of any type. Arrays are zero-indexed, meaning the first element is at index 0.

### Creating Arrays

```javascript
const arr = [1, 2, 3, 4, 5];
const arr2 = new Array(10); // creates an array with 10 undefined elements
```

### Accessing and Modifying Elements

```javascript
console.log(arr[0]); // Output: 1
arr[1] = 20; // Modify the second element
console.log(arr); // Output: [1, 20, 3, 4, 5]
```

### Common Array Methods

- **push**: Adds one or more elements to the end of an array.
  ```javascript
  arr.push(6); // [1, 20, 3, 4, 5, 6]
  ```
- **pop**: Removes the last element from an array.
  ```javascript
  arr.pop(); // [1, 20, 3, 4, 5]
  ```
- **shift**: Removes the first element from an array.
  ```javascript
  arr.shift(); // [20, 3, 4, 5]
  ```
- **unshift**: Adds one or more elements to the beginning of an array.
  ```javascript
  arr.unshift(0); // [0, 20, 3, 4, 5]
  ```
- **splice**: Adds or removes elements from an array.
  ```javascript
  arr.splice(2, 1); // Removes 1 element at index 2
  console.log(arr); // [0, 20, 4, 5]
  ```
- **slice**: Returns a shallow copy of a portion of an array.
  ```javascript
  const newArr = arr.slice(1, 3); // [20, 4]
  ```
- **forEach**: Executes a provided function once for each array element.
  ```javascript
  arr.forEach((item) => console.log(item));
  ```
- **map**: Creates a new array with the results of calling a provided function on every element.
  ```javascript
  const doubled = arr.map((item) => item * 2); // [0, 40, 8, 10]
  ```
- **filter**: Creates a new array with all elements that pass the test implemented by the provided function.
  ```javascript
  const even = arr.filter((item) => item % 2 === 0); // [0, 20, 4]
  ```
- **reduce**: Executes a reducer function on each element of the array, resulting in a single output value.
  ```javascript
  const sum = arr.reduce((acc, item) => acc + item, 0); // 29
  ```

## Objects

### Introduction

Objects are collections of key-value pairs. They are used to store data in a structured way.

### Creating Objects

```javascript
const obj = {
  name: "Alice",
  age: 25,
  isStudent: true,
};
```

### Accessing and Modifying Properties

```javascript
console.log(obj.name); // Output: Alice
obj.age = 26; // Modify the age property
console.log(obj); // { name: 'Alice', age: 26, isStudent: true }
```

### Common Object Methods

- **keys**: Returns an array of the object's own property names.
  ```javascript
  console.log(Object.keys(obj)); // ['name', 'age', 'isStudent']
  ```
- **values**: Returns an array of the object's own property values.
  ```javascript
  console.log(Object.values(obj)); // ['Alice', 26, true]
  ```
- **entries**: Returns an array of the object's own enumerable string-keyed property [key, value] pairs.
  ```javascript
  console.log(Object.entries(obj)); // [['name', 'Alice'], ['age', 26], ['isStudent', true]]
  ```
- **assign**: Copies all enumerable own properties from one or more source objects to a target object.
  ```javascript
  const newObj = Object.assign({}, obj, { gender: "female" });
  console.log(newObj); // { name: 'Alice', age: 26, isStudent: true, gender: 'female' }
  ```
- **hasOwnProperty**: Returns a boolean indicating whether the object has the specified property.
  ```javascript
  console.log(obj.hasOwnProperty("name")); // true
  ```

## Maps

### Introduction

Maps are collections of key-value pairs where the keys can be any datatype.

### Creating Maps

```javascript
const map = new Map();
```

### Setting and Getting Values

```javascript
map.set("name", "Alice");
map.set("age", 25);
console.log(map.get("name")); // Output: Alice
```

### Common Map Methods

- **set**: Adds or updates an element with a specified key and value.
  ```javascript
  map.set("isStudent", true);
  ```
- **get**: Returns the value associated with the specified key.
  ```javascript
  console.log(map.get("age")); // 25
  ```
- **has**: Returns a boolean indicating whether an element with the specified key exists.
  ```javascript
  console.log(map.has("name")); // true
  ```
- **delete**: Removes the element with the specified key.
  ```javascript
  map.delete("isStudent");
  ```
- **clear**: Removes all elements from the map.
  ```javascript
  map.clear();
  ```
- **size**: Returns the number of elements in the map.
  ```javascript
  console.log(map.size); // 0
  ```

### Iterating Over Maps

```javascript
map.set("name", "Alice");
map.set("age", 25);

for (const [key, value] of map) {
  console.log(`${key}: ${value}`);
}
// Output:
// name: Alice
// age: 25
```

## Sets

### Introduction

Sets are collections of unique values.

### Creating Sets

```javascript
const set = new Set();
```

### Adding and Checking Values

```javascript
set.add(1);
set.add(2);
set.add(2); // Duplicate values are ignored
console.log(set.has(2)); // true
console.log(set.has(3)); // false
```

### Common Set Methods

- **add**: Adds a new element to the set.
  ```javascript
  set.add(3);
  ```
- **has**: Returns a boolean indicating whether an element exists.
  ```javascript
  console.log(set.has(1)); // true
  ```
- **delete**: Removes the specified element from the set.
  ```javascript
  set.delete(2);
  ```
- **clear**: Removes all elements from the set.
  ```javascript
  set.clear();
  ```
- **size**: Returns the number of elements in the set.
  ```javascript
  console.log(set.size); // 0
  ```

### Iterating Over Sets

```javascript
set.add(1);
set.add(2);
set.add(3);

for (const value of set) {
  console.log(value);
}
// Output:
// 1
// 2
// 3
```

### Summary

- **Arrays**: Ordered collections of items.
- **Objects**: Collections of key-value pairs.
- **Maps**: Key-value pairs where keys can be of any datatype.
- **Sets**: Collections of unique values.
