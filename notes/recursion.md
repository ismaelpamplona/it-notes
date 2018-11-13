# Recursion

### YouTube Videos:

[Recursion - Part 7 of Functional Programming in JavaScript - FunFunFunction](https://www.youtube.com/watch?v=k7-N8R0-KY4)

[Recursion in software development - freeCodeCamp.org](https://www.youtube.com/watch?v=vPEJSJMg4jY)

[[BONUS] Debugging recursive functions—CMPUT 175 - CMPUT 175](https://www.youtube.com/watch?v=Btoobiaf5Gw)

```JavaScript
let factorial = (n) => {

  if (n<1) return 1;
  let prev =  factorial(n-1);
  return n*prev

}

console.log(factorial(3));
```

```JavaScript
let categories = [
  {id: "animals", "parent": null},
  {id: "mammals", "parent": "animals"},
  {id: "cats", "parent": "mammals"},
  {id: "dogs", "parent": "mammals"},
  {id: "chihuahua", "parent": "dogs"},
  {id: "labrador", "parent": "dogs"},
  {id: "persian", "parent": "cats"},
  {id: "siamese", "parent": "cats"}
];

// console.log(categories);

const makeTree = (categories, parent) => {
  let node = {};
  categories
    .filter(c => c.parent === parent)
    .forEach(c => node[c.id] = makeTree(categories, c.id));

 return node;
}

const show = (data) => {
  console.log(JSON.stringify(data, null, 2));
}

show(makeTree(categories, null))
```
