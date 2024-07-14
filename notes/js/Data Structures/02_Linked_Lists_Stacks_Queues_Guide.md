# Linked Lists, Stacks, and Queues in JavaScript

## Linked Lists

### Introduction

A linked list is a linear data structure where each element (node) contains a value and a reference (link) to the next node in the sequence.

### Types of Linked Lists

- **Singly Linked List**: Each node points to the next node.
- **Doubly Linked List**: Each node points to both the next and previous nodes.
- **Circular Linked List**: The last node points back to the first node.

### Singly Linked List Example

#### Node Class

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}
```

#### LinkedList Class

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.size = 0;
  }

  // Add a node at the end
  add(value) {
    const newNode = new Node(value);

    if (this.head === null) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next !== null) {
        current = current.next;
      }
      current.next = newNode;
    }
    this.size++;
  }

  // Remove a node
  remove(value) {
    let current = this.head;
    let previous = null;

    while (current !== null) {
      if (current.value === value) {
        if (previous === null) {
          this.head = current.next;
        } else {
          previous.next = current.next;
        }
        this.size--;
        return current.value;
      }
      previous = current;
      current = current.next;
    }
    return null;
  }

  // Print the linked list
  print() {
    let current = this.head;
    let result = "";
    while (current !== null) {
      result += current.value + " -> ";
      current = current.next;
    }
    console.log(result + "null");
  }
}

// Usage
const list = new LinkedList();
list.add(1);
list.add(2);
list.add(3);
list.print(); // 1 -> 2 -> 3 -> null
list.remove(2);
list.print(); // 1 -> 3 -> null
```

## Stacks

### Introduction

A stack is a linear data structure that follows the Last In, First Out (LIFO) principle. The last element added to the stack is the first one to be removed.

### Example

#### Stack Class

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  // Add an element to the stack
  push(element) {
    this.items.push(element);
  }

  // Remove and return the top element from the stack
  pop() {
    if (this.items.length === 0) {
      return "Underflow";
    }
    return this.items.pop();
  }

  // Return the top element without removing it
  peek() {
    if (this.items.length === 0) {
      return "No elements in Stack";
    }
    return this.items[this.items.length - 1];
  }

  // Check if the stack is empty
  isEmpty() {
    return this.items.length === 0;
  }

  // Print the stack
  printStack() {
    let str = "";
    for (let i = 0; i < this.items.length; i++) {
      str += this.items[i] + " ";
    }
    return str;
  }
}

// Usage
const stack = new Stack();
stack.push(10);
stack.push(20);
stack.push(30);
console.log(stack.printStack()); // 10 20 30
console.log(stack.pop()); // 30
console.log(stack.peek()); // 20
console.log(stack.printStack()); // 10 20
```

## Queues

### Introduction

A queue is a linear data structure that follows the First In, First Out (FIFO) principle. The first element added to the queue is the first one to be removed.

### Example

#### Queue Class

```javascript
class Queue {
  constructor() {
    this.items = [];
  }

  // Add an element to the queue
  enqueue(element) {
    this.items.push(element);
  }

  // Remove and return the front element from the queue
  dequeue() {
    if (this.isEmpty()) {
      return "Underflow";
    }
    return this.items.shift();
  }

  // Return the front element without removing it
  front() {
    if (this.isEmpty()) {
      return "No elements in Queue";
    }
    return this.items[0];
  }

  // Check if the queue is empty
  isEmpty() {
    return this.items.length === 0;
  }

  // Print the queue
  printQueue() {
    let str = "";
    for (let i = 0; i < this.items.length; i++) {
      str += this.items[i] + " ";
    }
    return str;
  }
}

// Usage
const queue = new Queue();
queue.enqueue(10);
queue.enqueue(20);
queue.enqueue(30);
console.log(queue.printQueue()); // 10 20 30
console.log(queue.dequeue()); // 10
console.log(queue.front()); // 20
console.log(queue.printQueue()); // 20 30
```

### Summary

- **Linked Lists**: Linear data structures where each element points to the next.
- **Stacks**: Linear data structures that follow the Last In, First Out (LIFO) principle.
- **Queues**: Linear data structures that follow the First In, First Out (FIFO) principle.
