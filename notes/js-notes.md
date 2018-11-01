# JavaScript Notes

### JavaScript

_JavaScript_, often abbreviated as JS, is a high-level, interpreted programming language. It is a language which is also characterized as dynamic, weakly typed, prototype-based and multi-paradigm.

Where dos JavaScript run? Browser and/or Server (Node.js)

[Oficial Documentation - https://developer.mozilla.org/en-US/docs/Web/javascript](https://developer.mozilla.org/en-US/docs/Web/javascript)

### ECMAScript (ES)

_ECMAScript_ is a trademarked scripting-language specification standardized by Ecma International in ECMA-262 and ISO/IEC 16262. It was created to standardize JavaScript, so as to foster multiple independent implementations.

### Variables

#### Null, Undefined and NaN

_NaN_: error message from a math calculation
In JS, _Null_ can not be compared to anything, except when: _Null_ is compared to _Undefined_

```javascript
null === undefined; // false
null == undefined; // true
null === null; // true

console.log(null == 0); // false
console.log(null == undefined); // true
console.log(NaN == NaN); // false

console.log(typeof NaN); // "number"
console.log(typeof null); // "object"
console.log(typeof undefined); // ¨undefined"
```

#### Scope - Declaring a variable without "var" - JS automatic generates a global variable

```javascript
function coco() {
    var test = "buceta"; // LOCAL VARIABLE w/ strict mode var
    console.log("inside the function - " + test);
}

coco(); // "inside the function - buceta"
console.log("outside the function - " + test); // "ReferenceError: test is not defined
```

```javascript
function coco() {
    test = "buceta"; // GLOBAL VARIABLE
    console.log("inside the function - " + test);
}

coco(); // "inside the function - buceta"
console.log("outside the function - " + test); // WORKS --> "outside the function - buceta"
```

### Hoisting

-   _Hoisting_ is JavaScript's default behavior of moving all declarations to the top of the current scope (to the top of the current script or the current function).
-   In JavaScript, a variable can be declared after it has been used.
-   In other words; a variable can be used before it has been declared.

### IF Statement

```javascript
var condition = 1;
var anotherCondition = false

if (condition) {
    console.log("Executed");
} else if (anotherCondition)
```

### Command: Do / While

```javascript
var condition = false;

do {
    console.log("buceta"); // "buceta" 1x
} while (condition);
```

### Multiplication and Floating Point Problems

In the real World 1.3 \* 2.2 = 2.86, but look...

```javascript
var a = 1.3;
var b = 2.2;

if (a * b == 2.86) {
    // ** the multiplication result is 2.860000000003
    console.log("true");
} else {
    console.log("false"); // ***
}
```

Fixing this problem:

```javascript
var a = 1.3;
var b = 2.2;

if ((a * b).toFixed(2) == 2.86) {
    // ** the multiplication result is 2.86
    console.log("true"); // ***
} else {
    console.log("false");
}
```

### Splice and Slice Methods

-   _Slice:_ does not modify the original array

    ```javascript
    var first_array = [1, 2, 3];
    var second_array = first_array.slice(1, 2); // start argument, and ends at (but does not include)
    console.log(first_array); // [1, 2, 3]
    console.log(second_array); // [2]
    ```

-   _Splice:_ does not modify the original array

    ```javascript
    var first_array = [1, 2, 3];
    var second_array = first_array.splice(1, 2); // first index and number of elements
    console.log(first_array); // [1]
    console.log(second_array); // [2, 3]
    ```

### Filter, Map, Reverse

-   _Filter and Map_ do not modify the original array, but return a new array. _Reverse_ modifies the original array.

    ```javascript
    var array = [1, 2, 3, 4];
    var filteredArray = array.filter(function(element) {
        return element > 1;
    });

    console.log(filteredArray); // [2, 3, 4]

    var mappedArray = array.map(function(element) {
        return element * 3;
    });

    console.log(mappedArray); // [3, 6, 9, 12]

    console.log(array.reverse()); // [4, 3, 2, 1]
    ```

### Concat and Join

-   _Concat_: allows to combine 2 arrays in 1 array. Do not modify the original array.

    ```javascript
    var array = [1, 2, 3, 4];
    var newArray = [a, b];
    console.log(array.concat(newArray)); // [1, 2, 3, 4, a, b]
    console.log(array); // [1, 2, 3, 4]
    console.log(newArray); // [a, b]
    ```

-   _Join_: transform the original array in a String and tell how the elements of the array will be separated in the String.

    ```javascript
    var array = [1, 2, 3, 4, 5];
    var secondArray = [" - "];
    console.log(array.join(secondArray)); // "1 - 2 - 3 - 4 - 5"
    ```

### Handling Erros with Try and Catch

    ```javascript
    try {
        ASDFASDFASDF() // function that does not exist - SOME ERROR
    } catch (error){
        console.log(error); //
    } finally {
        console.log('Finally');
    }
    ```

### Closures

    ```javascript
    function gen (input) {
        var num = input;
        return function () {
            return num * 2;
        }
    }
    var test = gen(20);
    var anotherTest = gen(40)
    console.log(test()) // 40
    console.log(anotherTest()) // 80
    ```

### Immediately Invoked Function Executions (IIFEs)

    ```javascript
    (function calc(input) {
        console.log("Calc: " + input);
    })(10);
    ```

### Built-in Methods & Properties

    ```javascript
    function calc (a, b, c) {
        console.log(a) // 1
        console.log(b) // 2
        console.log(c) // undefined
        console.log(arguments) // [object Arguments] { 0: 1, 1: 2 }
        return a+b+c
    }
    calc(1,2)
    console.log(calc.name) // "calc"
    console.log(calc.length) // 3
    ```

### DOM

MDN web docs - DOM: [Document Object Model (DOM)](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)

### Iterators in JavaScript

youtube: [Fun fun Function Channel - Iterators in JavaScript](https://www.youtube.com/watch?v=W4brAobC2Hc&list=PL0zVEGEvSaeG2T5n8FuPGb11JHea7idb9)
