
# Promises and async/await

## Promises

### What is a Promise?
A Promise is an object representing the eventual completion or failure of an asynchronous operation. Promises provide a way to handle asynchronous operations more efficiently than traditional callbacks.

### Creating a Promise
To create a Promise, you use the `Promise` constructor which takes a function with two parameters: `resolve` and `reject`.

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Asynchronous operation
  let success = true;

  if (success) {
    resolve("Operation was successful");
  } else {
    reject("Operation failed");
  }
});
```

### Using Promises
Promises have methods like `.then()`, `.catch()`, and `.finally()` to handle the results.

#### .then()
- Handles the resolved value.

```javascript
myPromise.then((result) => {
  console.log(result); // Output: "Operation was successful"
});
```

#### .catch()
- Handles the rejected value.

```javascript
myPromise.catch((error) => {
  console.error(error); // Output: "Operation failed"
});
```

#### .finally()
- Executes code regardless of whether the promise was resolved or rejected.

```javascript
myPromise.finally(() => {
  console.log("Operation completed");
});
```

### Chaining Promises
You can chain multiple `.then()` calls to handle a sequence of asynchronous operations.

```javascript
myPromise
  .then((result) => {
    console.log(result);
    return anotherPromise();
  })
  .then((newResult) => {
    console.log(newResult);
  })
  .catch((error) => {
    console.error(error);
  })
  .finally(() => {
    console.log("All operations completed");
  });
```

### Example with Promises
Here's a practical example using Promises:

```javascript
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const data = { user: "John", age: 30 };
      resolve(data);
    }, 2000);
  });
}

fetchData()
  .then((data) => {
    console.log("Data fetched:", data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

## async/await

### What is async/await?
`async` and `await` are syntactic sugar built on top of Promises. They make asynchronous code look and behave more like synchronous code, making it easier to read and maintain.

### Using async/await
- `async` keyword: Used to declare an asynchronous function.
- `await` keyword: Used to wait for a Promise to resolve or reject.

### Example with async/await

```javascript
async function fetchData() {
  try {
    const response = await new Promise((resolve, reject) => {
      setTimeout(() => {
        const data = { user: "John", age: 30 };
        resolve(data);
      }, 2000);
    });
    console.log("Data fetched:", response);
  } catch (error) {
    console.error("Error:", error);
  }
}

fetchData();
```

### Combining Promises and async/await

```javascript
async function fetchData() {
  try {
    const data = await getData();
    const processedData = await processData(data);
    console.log("Processed Data:", processedData);
  } catch (error) {
    console.error("Error:", error);
  } finally {
    console.log("Operation completed");
  }
}

function getData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve({ user: "John", age: 30 });
    }, 2000);
  });
}

function processData(data) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      data.processed = true;
      resolve(data);
    }, 1000);
  });
}

fetchData();
```

### Error Handling with async/await
Use try/catch blocks to handle errors in asynchronous functions.

```javascript
async function fetchData() {
  try {
    const response = await fetch("https://api.example.com/data");
    const data = await response.json();
    console.log("Data fetched:", data);
  } catch (error) {
    console.error("Error:", error);
  }
}

fetchData();
```

### Summary
- **Promises:** Objects representing the eventual completion or failure of an asynchronous operation. Methods: `.then()`, `.catch()`, `.finally()`.
- **async/await:** Syntactic sugar over Promises to write asynchronous code that looks synchronous. Use `try/catch` for error handling.
