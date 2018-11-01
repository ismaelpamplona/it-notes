# Big O Notation

### YouTube Videos:

[Big O Notation - HackerHank](https://www.youtube.com/watch?v=v4cd1O4zkGw)

"Big" means "capital", and "O" means order, as in "order of complexity". So named because of the convention of writing "order of complexity" as O(f(x)), e.g., with a capital letter 'O', or a 'Big O'.

## 4 Importants Rules - BigO

### 1 - Different steps get added

```JavaScript
function step1() {}

function step2() {}

function something() {

  step1(); // O(a)
  step2(); // O(b)
  // total runtime --> O(a+b)

}
```

### 2 - Drop constants

You do not write O(2n) or O(3n) because you are just looking how things scale roughly. It is a linear relashionship, it is a quadradic relationship - _So you always drop constants_

```JavaScript
var myArr = [1, 2, 3, 4, 5, 6]

function minMax1(arr) { // O(n) and not O(2n), in BigO you have do drop the constants
  var min = null;
  var max = null;

  for (i in arr) {
    min = Math.min(arr[i], min);
  }

  for (i in arr) {
    max = Math.max(arr[i], max);
  }
}

minMax1(myArr);


function minMax2(arr){ // O(n)
  var min = null;
  var max = null;

  for (i in arr) {
    min = Math.min(arr[i], min);
    max = Math.max(arr[i], max);
  }
 }

minMax2(myArr)
```

### 3 - Different inputs ==> Different variables

```JavaScript
var myArrA = ["a", "b", "c", "d", "e", "f"];
var myArrB = ["c", "d", "f", "g", "h"];

function intersectionSize(arrA, arrB) {
  var count = 0;

  for (a in arrA){ // O(a)
    for (b in arrB) { // O(b)
      if (arrA[a] == arrB[b]) {
        count++
      }
    }
  }
  return count
} // total runtime is O(a*b) and not O(n²)

console.log(intersectionSize(myArrA, myArrB))
```

### 4 - Drop non-dominate terms

You have to drop the non-dominate terms. In the example above: O(n+n²) becomes O(n²)

```JavaScript
var myArr = [1, 2, 3, 4, 5, 6]

function nonSenseFunction(arr) {
  var max = null;

  for (a in arr) { // O(n)
    max = Math.max(a, max)
  }

  for (a in arr) { // O(n²)
    for (b in arr) {
      console.log(a + " - " + b);
    }
  }
}

nonSenseFunction(myArr);
```

## Examples in JS

```JavaScript
// Big O Notation

var myArr = ["a", "b", "c", "d", "e", "f"]

// O(n)

function contains(arr, x) {
  for (i in arr) {
    if (arr[i] == x) {
      var xPosition = i*1+1
      console.log (x + " is the " + xPosition + "° element of the array --> " + arr)
      return true
    }
  }
  console.log("the array does not contain the element ==> " + x)
}

contains (myArr, "c")


// \O(n²)

for (x in myArr) {
  for (y in myArr) {
//     console.log(myArr[x] + ", "+ myArr[y])
  }
}
```
