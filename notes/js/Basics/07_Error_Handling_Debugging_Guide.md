
# Error Handling and Debugging

## Error Handling

### try...catch Statement
The `try...catch` statement allows you to handle exceptions gracefully. Code that might throw an exception is placed in the `try` block, and the `catch` block contains code that handles the exception if one occurs.

#### Syntax
```javascript
try {
  // Code that may throw an error
} catch (error) {
  // Code to handle the error
}
```

#### Example
```javascript
try {
  let result = riskyOperation();
  console.log(result);
} catch (error) {
  console.error('An error occurred:', error.message);
}
```

### finally Block
The `finally` block can be added to execute code after the `try` and `catch` blocks, regardless of whether an exception was thrown or caught.

#### Syntax
```javascript
try {
  // Code that may throw an error
} catch (error) {
  // Code to handle the error
} finally {
  // Code to be executed regardless of an error
}
```

#### Example
```javascript
try {
  let result = riskyOperation();
  console.log(result);
} catch (error) {
  console.error('An error occurred:', error.message);
} finally {
  console.log('Execution completed.');
}
```

### throw Statement
The `throw` statement allows you to create custom errors.

#### Syntax
```javascript
throw new Error('Custom error message');
```

#### Example
```javascript
function riskyOperation() {
  if (Math.random() < 0.5) {
    throw new Error('Operation failed');
  }
  return 'Success';
}

try {
  let result = riskyOperation();
  console.log(result);
} catch (error) {
  console.error('An error occurred:', error.message);
}
```

### Custom Error Types
You can create custom error types by extending the `Error` class.

#### Example
```javascript
class CustomError extends Error {
  constructor(message) {
    super(message);
    this.name = 'CustomError';
  }
}

try {
  throw new CustomError('Something went wrong');
} catch (error) {
  console.error(error.name + ': ' + error.message);
}
```

## Debugging

### Using console.log
The simplest way to debug is using `console.log` to print messages to the console.

#### Example
```javascript
let value = 42;
console.log('The value is', value);
```

### Using console.error, console.warn, and console.info
You can use `console.error`, `console.warn`, and `console.info` to print messages with different levels of severity.

#### Example
```javascript
console.error('This is an error message');
console.warn('This is a warning message');
console.info('This is an info message');
```

### Debugger Statement
The `debugger` statement can be used to pause the execution of JavaScript and start debugging.

#### Example
```javascript
function debugExample() {
  let x = 10;
  debugger; // Execution will pause here
  let y = 20;
  return x + y;
}

debugExample();
```

### Using Browser Developer Tools
Most modern browsers have built-in developer tools that provide a comprehensive set of debugging features. These tools can be accessed using `F12` or `Ctrl+Shift+I`.

#### Features
- **Elements Panel**: Inspect and modify HTML and CSS.
- **Console Panel**: View and interact with JavaScript logs and errors.
- **Sources Panel**: Set breakpoints, step through code, and view the call stack.
- **Network Panel**: Monitor network requests and responses.
- **Performance Panel**: Analyze runtime performance.
- **Application Panel**: Inspect storage, cookies, and more.

### Setting Breakpoints
You can set breakpoints in the Sources panel to pause execution at specific lines of code.

#### Example
1. Open Developer Tools.
2. Go to the Sources panel.
3. Navigate to the JavaScript file.
4. Click on the line number where you want to set a breakpoint.

### Step-Through Debugging
Once a breakpoint is hit, you can use the following controls to debug your code:
- **Step Over (F10)**: Move to the next line of code.
- **Step Into (F11)**: Step into a function call.
- **Step Out (Shift+F11)**: Step out of the current function.

### Watching Variables
You can add variables to the Watch panel to monitor their values as you step through your code.

### Call Stack
The Call Stack panel shows the current function call stack, helping you trace the sequence of function calls that led to the current point of execution.

### Example: Using Browser Developer Tools

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Debugging Example</title>
</head>
<body>
  <script>
    function multiply(a, b) {
      return a * b;
    }

    function square(n) {
      return multiply(n, n);
    }

    function main() {
      let result = square(5);
      console.log('The result is', result);
    }

    main();
  </script>
</body>
</html>
```

1. Open the page in a browser.
2. Open Developer Tools (F12).
3. Go to the Sources panel and set a breakpoint inside the `multiply` function.
4. Refresh the page and use the debugging controls to step through the code.

### Summary

- **try...catch**: Handle exceptions.
- **finally**: Execute code regardless of exceptions.
- **throw**: Create custom errors.
- **Custom Error Types**: Extend the `Error` class for specific error types.
- **console.log, console.error, console.warn, console.info**: Print messages to the console.
- **debugger**: Pause code execution for debugging.
- **Browser Developer Tools**: Use for comprehensive debugging features.
- **Breakpoints**: Pause execution at specific lines of code.
- **Step-Through Debugging**: Control code execution flow.
- **Watching Variables**: Monitor variable values.
- **Call Stack**: Trace function calls.
