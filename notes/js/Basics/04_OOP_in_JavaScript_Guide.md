# Object-Oriented Programming (OOP) in JavaScript

## Introduction to OOP

Object-Oriented Programming (OOP) is a programming paradigm centered around objects rather than functions and logic. Objects are instances of classes, which can contain both data (attributes/properties) and methods (functions).

## Key Concepts

- **Class:** A blueprint for creating objects (instances).
- **Instance:** An object created from a class.
- **Constructors:** A special method for creating and initializing an object created within a class.
- **Methods:** Functions defined inside a class that describe the behaviors of the objects.
- **Inheritance:** A mechanism for one class to extend another class, inheriting its properties and methods.
- **Encapsulation:** The bundling of data with methods that operate on that data, restricting direct access to some of the object's components.
- **Polymorphism:** The ability to present the same interface for different underlying forms (data types).
- **Abstraction:** Hiding the complex implementation details and showing only the necessary features.

## Example of OOP in JavaScript

### Creating a Class

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(
      `Hello, my name is ${this.name} and I am ${this.age} years old.`
    );
  }
}

const john = new Person("John", 30);
john.greet(); // Hello, my name is John and I am 30 years old.
```

### Inheritance

```javascript
class Employee extends Person {
  constructor(name, age, jobTitle) {
    super(name, age);
    this.jobTitle = jobTitle;
  }

  greet() {
    console.log(
      `Hello, my name is ${this.name}, I am ${this.age} years old and I work as a ${this.jobTitle}.`
    );
  }
}

const jane = new Employee("Jane", 28, "Software Engineer");
jane.greet(); // Hello, my name is Jane, I am 28 years old and I work as a Software Engineer.
```

### Encapsulation

Encapsulation can be implemented using closures or the `#` symbol for private fields (introduced in ES2022).

```javascript
class BankAccount {
  #balance = 0; // private field

  constructor(accountNumber) {
    this.accountNumber = accountNumber;
  }

  deposit(amount) {
    if (amount > 0) {
      this.#balance += amount;
      console.log(`Deposited ${amount}, new balance is ${this.#balance}`);
    }
  }

  withdraw(amount) {
    if (amount > 0 && amount <= this.#balance) {
      this.#balance -= amount;
      console.log(`Withdrew ${amount}, new balance is ${this.#balance}`);
    } else {
      console.log("Insufficient funds");
    }
  }

  getBalance() {
    return this.#balance;
  }
}

const myAccount = new BankAccount("123456");
myAccount.deposit(500);
myAccount.withdraw(200);
console.log(myAccount.getBalance()); // 300
console.log(account.#balance); // Error: Private field '#balance' must be declared in an enclosing class
```

### Polymorphism

Polymorphism allows methods to be used interchangeably when they share the same name but operate on different data types.

```javascript
class Animal {
  speak() {
    console.log("The animal makes a sound");
  }
}

class Dog extends Animal {
  speak() {
    console.log("The dog barks");
  }
}

class Cat extends Animal {
  speak() {
    console.log("The cat meows");
  }
}

const animals = [new Animal(), new Dog(), new Cat()];
animals.forEach((animal) => animal.speak());
// Output:
// The animal makes a sound
// The dog barks
// The cat meows
```
