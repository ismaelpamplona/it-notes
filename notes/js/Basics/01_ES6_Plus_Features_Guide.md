# ES6+ Features

## let and const

- **let:** Block-scoped variable declaration. It allows reassignments.

  ```javascript
  let x = 10;
  x = 20; // Allowed
  ```

- **const:** Block-scoped variable declaration. It does not allow reassignments.
  ```javascript
  const y = 10;
  y = 20; // Error: Assignment to constant variable.
  ```

## Arrow Functions

- Shorter syntax for writing functions. It does not have its own `this`.
  ```javascript
  const add = (a, b) => a + b;
  ```

## Template Literals

- Allows embedding expressions within strings using backticks.
  ```javascript
  const name = "John";
  const greeting = `Hello, ${name}!`;
  ```

## Default Parameters

- Allows setting default values for function parameters.
  ```javascript
  function greet(name = "Guest") {
    console.log(`Hello, ${name}`);
  }
  ```

## Destructuring Assignment

- Extract values from arrays or properties from objects into distinct variables.

  ```javascript
  // Array Destructuring
  const [a, b] = [1, 2];

  // Object Destructuring
  const { name, age } = { name: "John", age: 30 };
  ```

## Rest and Spread Operators

- **Rest Operator (`...`):** Collects all remaining elements into an array.

  ```javascript
  function sum(...numbers) {
    return numbers.reduce((acc, num) => acc + num, 0);
  }

  sum(1, 2, 3, 4, 5);
  ```

  The numbers parameter will now be an array containing `[1, 2, 3, 4, 5]`.

- **Spread Operator (`...`):** Expands an array or object into individual elements.

  ```javascript
  const arr = [1, 2, 3];
  const newArr = [...arr, 4, 5];

  const obj = { a: 1, b: 2 };
  const newObj = { ...obj, c: 3 };
  ```

## Enhanced Object Literals

- Shorthand for defining properties and methods.

  ```javascript
  const name = "John";
  const age = 30;

  const person = {
    name,
    age,
    greet() {
      console.log(`Hello, ${this.name}`);
    },
  };
  ```

## Promises

- Asynchronous programming using promises.

  ```javascript
  const fetchData = () => {
    return new Promise((resolve, reject) => {
      // Simulate async operation
      setTimeout(() => {
        resolve("Data fetched");
      }, 1000);
    });
  };

  fetchData().then((data) => console.log(data));
  ```

## Async/Await

- Syntactic sugar for Promises, making asynchronous code look synchronous.

  ```javascript
  const fetchData = async () => {
    const data = await fetch("https://api.example.com/data");
    const json = await data.json();
    console.log(json);
  };

  fetchData();
  ```

## Classes

- Syntactic sugar over prototypes for object-oriented programming.

  ```javascript
  class Person {
    constructor(name, age) {
      this.name = name;
      this.age = age;
    }

    greet() {
      console.log(`Hello, my name is ${this.name}`);
    }
  }

  const john = new Person("John", 30);
  john.greet();
  ```

## Modules

- Import and export functionalities between different files.

  ```javascript
  // In file person.js
  export const name = "John";
  export const age = 30;

  // In file main.js
  import { name, age } from "./person.js";
  console.log(name, age);
  ```

## Iterators and Generators

- **Iterators:** Objects with a `next()` method that returns `{ value, done }`.

  ```javascript
  const iterable = {
    [Symbol.iterator]() {
      let step = 0;
      return {
        next() {
          step++;
          if (step <= 3) {
            return { value: step, done: false };
          }
          return { value: undefined, done: true };
        },
      };
    },
  };

  for (const value of iterable) {
    console.log(value);
  }
  ```

- **Generators:** Functions that can be paused and resumed.

  ```javascript
  function* generatorFunction() {
    yield 1;
    yield 2;
    yield 3;
  }

  const generator = generatorFunction();
  console.log(generator.next().value); // 1
  console.log(generator.next().value); // 2
  console.log(generator.next().value); // 3
  ```

## Map, Set, WeakMap, WeakSet

- **Map:** Collection of keyed data items, like an Object, but keys can be of any type.

  ```javascript
  const map = new Map();
  map.set("key", "value");
  console.log(map.get("key")); // 'value'
  ```

- **Set:** Collection of unique values.

  ```javascript
  const set = new Set([1, 2, 3, 3]);
  console.log(set.has(3)); // true
  console.log(set.size); // 3
  ```

- **WeakMap and WeakSet:** Similar to Map and Set but with weak references to objects.

## Symbol

- Unique and immutable primitive value used as the key of an object property.
  ```javascript
  const sym = Symbol("description");
  const obj = {
    [sym]: "value",
  };
  console.log(obj[sym]); // 'value'
  ```

## Array Methods

- New methods added to Array prototype.

  ```javascript
  // Array.from
  const arr = Array.from("hello"); // ['h', 'e', 'l', 'l', 'o']

  // Array.find
  const found = [1, 2, 3].find((num) => num > 1); // 2

  // Array.includes
  const includesTwo = [1, 2, 3].includes(2); // true
  ```
