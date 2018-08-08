# JavaScript Notes

### JavaScript

**JavaScript**, often abbreviated as JS, is a high-level, interpreted programming language. It is a language which is also characterized as dynamic, weakly typed, prototype-based and multi-paradigm.

Where dos JavaScript run? Browser and/or Server (Node.js)

### ECMAScript (ES)

ECMAScript is a trademarked scripting-language specification standardized by Ecma International in ECMA-262 and ISO/IEC 16262. It was created to standardize JavaScript, so as to foster multiple independent implementations.

### Variables

#### Null, Undefined and NaN

**NaN** = error message from a math calculation

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

### Hoisting

-   _Hoisting_ is JavaScript's default behavior of moving all declarations to the top of the current scope (to the top of the current script or the current function).
-   In JavaScript, a variable can be declared after it has been used.
-   In other words; a variable can be used before it has been declared.

### Command: Do / While

    ```javascript
    var condition = false;

    do {
        console.log("buceta"); // "buceta" 1x
    } while (condition);
    ```

### Scope - Declaring a variable without "var" - JS automatic generates a global variable

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

-   _Concat_ allows to combine 2 arrays in 1 array. Do not modify the original array.

    ```javascript
    var array = [1, 2, 3, 4];
    var newArray = [a, b];
    console.log(array.concat(newArray)); // [1, 2, 3, 4, a, b]
    console.log(arra); // [1, 2, 3, 4]
    console.log(newArray); // [a, b]
    ```

-   _Join_ transform the original array in a String and tell how the elements of the array will be separated in the String.

    ```javascript
    var array = [1, 2, 3, 4, 5];
    var secondArray = [" - "];
    console.log(array.join(secondArray)); // "1 - 2 - 3 - 4 - 5"
    ```
