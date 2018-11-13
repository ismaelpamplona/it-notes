# Stacks

### YouTube Videos:

[Stacks (Data Structure) - Beau teaches JavaScript - freeCodeCamp.org](https://www.youtube.com/watch?v=Gj5qBheGOEo&list=PLWKjhJtqVAbkso-IbgiiP48n-O-JQA9PJ)

### Stacks in JS

```JavaScript
/* Stacks! */

// functions: push, pop, peek, length

var Stack = function(){

  this.len = 0;/* Stacks! */

// functions: push, pop, peek, length

var chars = []; // this is our stack

var word = "racecar"

var rword = "";

// put chars of word into stack
for (var i = 0; i < word.length; i++) {
   chars.push(word[i]);
}

// pop off the stack in reverse order
for (var i = 0; i < word.length; i++) {
   rword += chars.pop();
}

if (rword === word) {
   console.log(word + " is a palindrome.");
}
else {
   console.log(word + " is not a palindrome.");
}

```

```JavaScript

// Creates a stack
class Stack {

  constructor(){
    this.storage = {};
    this.count = 0;
  }

  push(data) {
    this.storage[this.count] = data;
    this.count++;
  }

  pop(){
    if (this.count === 0) return undefined;
    this.count--;
    const result = this.storage[this.count];
    delete this.storage[this.count];
    return result;
  }

  peek(){
    return this.storage[this.count-1];
  }

  size(){
    return this.count;
  }

}

const myStack = new Stack();

console.log(myStack);
myStack.push("Book 1");
myStack.push("Book 2");
myStack.push("Book 3");
console.log(myStack);
myStack.pop();
console.log(myStack);
console.log(myStack.size());
console.log(myStack.peek());
```
