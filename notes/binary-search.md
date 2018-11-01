# Binary Search

### YouTube Videos:

[Algorithms: Binary Search - HackerRank Channel](https://www.youtube.com/watch?v=P3YID7liBug)

```javascript
// Binary Search Array

var myArray = [7, 9, 5, 1, 3, 10, 13];

var findMyNumber = function(arr, num) {
    console.log(
        "#############################################################"
    );

    console.log("arr: " + arr);

    var sortedArray = arr.concat().sort((a, b) => {
        //This method does not change the existing arrays, but returns a new array, containing the values of the joined arrays
        return a - b;
    });

    // In binary search the array must be sorted

    console.log("sortedArray: " + sortedArray);
    console.log("the number to be founded is: " + num);

    var left = 0;
    var right = myArray.length - 1;

    var i = 0;

    while (left <= right) {
        i++;
        console.log(i + "° while loop");
        console.log("left: " + left);
        console.log("right: " + right);

        var mid = parseInt((left + right) / 2);
        console.log("mid: " + mid);
        console.log("num: " + num);
        console.log("arr[mid]: " + arr[mid]);

        if (num == sortedArray[mid]) {
            console.log("Number --> " + num + " <-- FOUNDED !!!");
            return true;
        }

        if (num < sortedArray[mid]) {
            console.log(num + " is less than " + "arr[mid]");
            right = mid - 1;
            console.log("new right = " + right);
        }

        if (num > sortedArray[mid]) {
            console.log(num + " is greater than " + arr[mid]);
            left = mid + 1;
            console.log("new left = " + left);
        }

        console.log("---- " + i + "° while loop end ----");
    }

    console.log(num + " NOT FOUNDED !!!");

    return false;
};

myArray.map(e => {
    findMyNumber(myArray, e);
});

findMyNumber(myArray, 0);

findMyNumber(myArray, 3.5);

findMyNumber(myArray, 15);

findMyNumber(myArray, -15);
```

```javascript
// Find the minimum element in an array.

var myArray = [7, 9, 5, 1, 3, 10, 13];

var findTheMinElement = function(arr) {
    var min = arr[0];
    arr.map((e, i) => {
        if (e < min) {
            min = e;
        }
    });
    return min;
};

console.log(findTheMinElement(myArray));
```
