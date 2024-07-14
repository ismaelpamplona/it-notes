# Event Handling

Event handling in JavaScript involves writing code that responds to user interactions with the web page, such as clicks, key presses, and mouse movements. Here’s an overview of the most important aspects of event handling.

## Common Event Types

- **Mouse Events**: `click`, `dblclick`, `mousedown`, `mouseup`, `mouseover`, `mouseout`, `mousemove`
- **Keyboard Events**: `keydown`, `keyup`, `keypress`
- **Form Events**: `submit`, `change`, `focus`, `blur`
- **Window Events**: `load`, `resize`, `scroll`

## Adding Event Listeners

To respond to events, you use event listeners. An event listener is a function that is executed when an event occurs.

```js
const button = document.getElementById("myButton");

// Add event listener for 'click' event
button.addEventListener("click", () => {
  alert("Button was clicked!");
});
```

## Removing Event Listeners

To remove an event listener, use the `removeEventListener` method. The function that was originally passed to `addEventListener` must be referenced when removing it.

```js
const button = document.getElementById("myButton");

const handleClick = () => {
  alert("Button was clicked!");
};

// Add event listener for 'click' event
button.addEventListener("click", handleClick);

// Remove event listener
button.removeEventListener("click", handleClick);
```

## Event Object

When an event occurs, an event object is automatically passed to the event handler. This object contains useful information about the event.

```js
const button = document.getElementById("myButton");

// Add event listener for 'click' event
button.addEventListener("click", (event) => {
  console.log("Event type:", event.type); // Output: Event type: click
  console.log("Button text:", event.target.textContent); // Output: Button text: Click Me
});
```

## Event Delegation

Event delegation involves using a single event listener to manage events for multiple elements. This is efficient for handling events on many elements.

```js
const list = document.getElementById("myList");

// Add event listener to the parent element
list.addEventListener("click", (event) => {
  if (event.target.tagName === "LI") {
    alert("Clicked on: " + event.target.textContent);
  }
});
```

## Preventing Default Behavior

To prevent the default behavior of an element, use the `preventDefault` method on the event object.

```js
const link = document.getElementById("myLink");

// Add event listener to the link
link.addEventListener("click", (event) => {
  event.preventDefault(); // Prevent the default action of the link
  alert("Link was clicked, but default action was prevented.");
});
```

## Event Propagation

Event propagation refers to the way events travel through the DOM hierarchy. It occurs in three phases:

1.  **Capturing Phase**: The event starts from the root and travels down to the target element.
2.  **Target Phase**: The event reaches the target element.
3.  **Bubbling Phase**: The event travels back up to the root from the target element.

By default, most events bubble up the DOM tree, meaning they are first captured by the target element and then propagated to its parent elements.

### Stop propagation

`stopPropagation` prevents further propagation of the current event in the capturing and bubbling phases. This means that the event won't be passed on to any parent elements.

```js
const outerDiv = document.getElementById("outerDiv");
const innerDiv = document.getElementById("innerDiv");

outerDiv.addEventListener("click", () => {
  alert("Outer Div clicked");
});

innerDiv.addEventListener("click", (event) => {
  alert("Inner Div clicked");
  event.stopPropagation(); // Stops the event from propagating to the outer div
});
```

In this example, clicking on the `innerDiv` triggers its alert, but the event does not propagate to the `outerDiv` because `stopPropagation` is called.

### Stop Immediate Propagation

`stopImmediatePropagation` prevents other listeners of the same event from being called on the same element. This means it stops the event from propagating and also prevents any other event listeners on the same element from executing.

```js
const button = document.getElementById("myButton");

button.addEventListener("click", () => {
  alert("First listener");
});

button.addEventListener("click", (event) => {
  alert("Second listener");
  event.stopImmediatePropagation(); // Stops other listeners from being executed
});

button.addEventListener("click", () => {
  alert("Third listener");
});
```

In this example, clicking the button triggers the first and second listeners, but the third listener is not executed because `stopImmediatePropagation` is called in the second listener.

## Summary

- **Common Event Types**: Mouse events, keyboard events, form events, and window events.
- **Adding Event Listeners**: Use `addEventListener` to attach an event handler to an element.
- **Removing Event Listeners**: Use `removeEventListener` to detach an event handler.
- **Event Object**: Contains information about the event and is automatically passed to the event handler.
- **Event Delegation**: Use a single event listener to manage events for multiple elements efficiently.
- **Preventing Default Behavior**: Use `preventDefault` to prevent the default action of an element.
