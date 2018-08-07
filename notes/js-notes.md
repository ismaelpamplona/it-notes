# JS Notes

Where dos JAvaScript run? Browser and/or Server (Node.js)

### ECMAScript (ES)

ECMAScript is a trademarked scripting-language specification standardized by Ecma International in ECMA-262 and ISO/IEC 16262. It was created to standardize JavaScript, so as to foster multiple independent implementations.

### JavaScript

**JavaScript**, often abbreviated as JS, is a high-level, interpreted programming language. It is a language which is also characterized as dynamic, weakly typed, prototype-based and multi-paradigm.

### Variables

```javascript
null === undefined; // false
null == undefined; // true
null === null; // true
```

NaN = error message from a math calculation

```javascript
typeof NaN; // "number"`
```

typeof null // "object"
typeof undefined // ¨undefined"

Hoisting

     In JavaScript, a variable can be declared after it has been used.

     In other words; a variable can be used before it has been declared.

     Hoisting is JavaScript's default behavior of moving all declarations to the top of the current scope (to the top of the current script or the current function).

Command: Do / While

     var condition = false;

     do {
        console.log("buceta");
     }
     while(condition);

    // "buceta" 1x

Null, Undefined and NaN

console.log(null == 0) // false

console.log(null == undefined) // true

console.log(NaN == NaN) // false

Scope - Declaring a variable without "var" - automatic JS generates a globalcariable

     function coco() {
         vart test = 'buceta'; // LOCAL VARIBLE w/ strict mode var
         console.log('inside the function - ' + test);
     }

     coco();
     console.log('outside the function - ' + test); // ERROR

     function coco() {
         test = 'buceta'; // GLOBAL VARIABLE
         console.log('inside the function - ' + test);
     }

     coco();
     console.log('outside the function - ' + test); / WORKS,

Splice and Slice Methods

     // Slice: does not modify the original array
        var first_array = [1, 2, 3];
        var second_array = first_array.slice(1,2); // index
        console.log(first_array); // [1, 2, 3]
        console.log(second_array) // [2]

     // Splice: does not modify the original array
        var first_array = [1, 2, 3]
        var second_array = first_array.splice(1,2) // first index and number of elements
        console.log(first_array) // [1]
        console.log(second_array) // [2, 3]

iaraujo

Filter, Map, Reverse

    Filter and Map do not modify the array, but return a new array.
    Reverse modifies the original array.

    var array = [1, 2, 3, 4]
    var filteredArray = array.filter(function(element){
        return element > 1
     })
    console.log(filteredArray) // [2, 3, 4]

    var mappedArray = array.map(function(element){
        return element * 3
     })
    console.log(mappedArray ) // [3, 6, 9, 12]

    console.log(array.reverse()) // [4, 3, 2, 1]

Concat and Join

     Concat allows to combine 2 arrays in 1 array. Do not modify the original array.

          (ar array = [1, 2, 3, 4]
         var newArray = [a, b]
         console.log(array.concat(newArray)) // [1, 2, 3, 4, a, b]
          console.log(arra) // [1, 2, 3, 4]
           console.log(newArray) // [a, b]

    Join transform the original array in a String and tell how the elements of the array will be separated in the String.

     var array = [1, 2, 3, 4, 5]
     var secondArray = [" - "]
     console.log(array.join(secondArray)) // "1 - 2 - 3 - 4 - 5"
