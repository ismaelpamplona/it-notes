# Node.js

Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. It allows developers to run JavaScript on the server side, making it possible to build scalable and high-performance applications.

## Key Features of Node.js

- **Non-blocking, event-driven architecture**: Handles many connections simultaneously.
- **Single-threaded**: Uses a single thread for event loops, but can utilize multiple cores using worker threads.
- **Asynchronous programming**: Supports asynchronous I/O operations.

## Node.js Architecture

Node.js uses a single-threaded event loop model to handle multiple connections. The event loop handles all asynchronous operations and executes callbacks when the operations are complete.

### Event Loop

The event loop is a core part of Node.js that handles I/O operations and ensures that the application remains responsive.

## Modules in Node.js

Node.js uses modules to organize code. Modules are reusable blocks of code that can be loaded and used in other parts of an application.

### CommonJS Modules

Node.js uses the CommonJS module system. Each file is a module with its own scope.

### Example

```javascript
// myModule.js
function sayHello() {
  console.log("Hello, world!");
}

module.exports = sayHello;
```

```javascript
// main.js
const sayHello = require("./myModule");
sayHello(); // Output: Hello, world!
```

### ES6 Modules

Node.js also supports ES6 modules using the `import` and `export` syntax.

### Example

```javascript
// myModule.mjs
export function sayHello() {
  console.log("Hello, world!");
}
```

```javascript
// main.mjs
import { sayHello } from "./myModule.mjs";
sayHello(); // Output: Hello, world!
```

## Core Modules

Node.js comes with several core modules that provide various functionalities.

### File System (fs)

The `fs` module provides an API for interacting with the file system.

### Example

```javascript
const fs = require("fs");

// Asynchronous read
fs.readFile("example.txt", "utf8", (err, data) => {
  if (err) throw err;
  console.log(data);
});

// Synchronous read
const data = fs.readFileSync("example.txt", "utf8");
console.log(data);
```

### HTTP

The `http` module allows you to create web servers and handle HTTP requests and responses.

### Example

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello, world!
');
});

server.listen(3000, '127.0.0.1', () => {
  console.log('Server running at http://127.0.0.1:3000/');
});
```

### Path

The `path` module provides utilities for working with file and directory paths.

### Example

```javascript
const path = require("path");

const filePath = "/users/test/file.txt";
console.log(path.dirname(filePath)); // /users/test
console.log(path.basename(filePath)); // file.txt
console.log(path.extname(filePath)); // .txt
```

## Event-Driven Model

Node.js is designed to be event-driven, meaning that it uses events to handle asynchronous operations.

### Example

```javascript
const EventEmitter = require("events");
const emitter = new EventEmitter();

emitter.on("event", () => {
  console.log("An event occurred!");
});

emitter.emit("event"); // Output: An event occurred!
```

## Asynchronous Programming

Node.js heavily relies on asynchronous programming. It uses callbacks, promises, and async/await to handle asynchronous operations.

### Callbacks

A callback is a function passed as an argument to another function, to be executed after the completion of some operation.

### Example

```javascript
function fetchData(callback) {
  setTimeout(() => {
    callback("Data fetched");
  }, 1000);
}

fetchData((data) => {
  console.log(data); // Output: Data fetched
});
```

### Promises

A promise represents the eventual completion (or failure) of an asynchronous operation and its resulting value.

### Example

```javascript
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Data fetched");
    }, 1000);
  });
}

fetchData()
  .then((data) => {
    console.log(data); // Output: Data fetched
  })
  .catch((error) => {
    console.error(error);
  });
```

### Async/Await

Async/await is syntactic sugar built on promises, making asynchronous code look and behave more like synchronous code.

### Example

```javascript
async function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Data fetched");
    }, 1000);
  });
}

async function main() {
  try {
    const data = await fetchData();
    console.log(data); // Output: Data fetched
  } catch (error) {
    console.error(error);
  }
}

main();
```

## Packages and npm

Node.js uses npm (Node Package Manager) to manage packages. npm allows you to install and manage dependencies for your Node.js applications.

### Installing Packages

```bash
npm install package-name
```

### Example

```bash
npm install express
```

## Creating a Simple Web Server with Express

Express is a popular web framework for Node.js.

### Example

```javascript
const express = require("express");
const app = express();

app.get("/", (req, res) => {
  res.send("Hello, world!");
});

app.listen(3000, () => {
  console.log("Server running on http://localhost:3000");
});
```

## Summary

- **Node.js**: JavaScript runtime built on Chrome's V8 engine.
- **Event Loop**: Handles asynchronous operations.
- **Modules**: Organized code into reusable blocks (CommonJS and ES6 modules).
- **Core Modules**: Built-in modules like `fs`, `http`, and `path`.
- **Event-Driven Model**: Uses events to handle asynchronous operations.
- **Asynchronous Programming**: Uses callbacks, promises, and async/await.
- **npm**: Manages packages and dependencies.
- **Express**: Popular framework for building web applications.
