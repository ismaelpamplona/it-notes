# DOM Manipulation

## What is the DOM?

The Document Object Model (DOM) is a programming interface for web documents. It represents the page so that programs can change the document structure, style, and content. The DOM is an object-oriented representation of the web page, which can be modified with a scripting language like JavaScript.

```
.
└── Document/
    └── html (Element)/
        ├── head (Element)/
        │   └── title (Element)/
        │       └── Text Node
        └── body (Element)/
            ├── header (Element)/
            │   └── h1 (Element)/
            │       └── Text Node
            ├── main (Element)/
            │   └── p (Element)/
            │       └── Text Node
            └── footer (Element)/
                └── p (Element)/
                    └── Text Node
```

## Common DOM Manipulation Tasks

### Selecting Elements

To manipulate elements, you first need to select them. There are several methods to select elements:

1. **getElementById**

   ```javascript
   const element = document.getElementById("myElementId");
   ```

2. **getElementsByClassName**

   ```javascript
   const elements = document.getElementsByClassName("myClassName");
   ```

3. **getElementsByTagName**

   ```javascript
   const elements = document.getElementsByTagName("div");
   ```

4. **querySelector**

   ```javascript
   const element = document.querySelector(".myClassName"); // Selects the first element with the class
   ```

5. **querySelectorAll**
   ```javascript
   const elements = document.querySelectorAll(".myClassName"); // Selects all elements with the class
   ```

### Changing Content

1. **innerHTML**

   ```javascript
   const element = document.getElementById("myElementId");
   element.innerHTML = "New Content";
   ```

2. **textContent**
   ```javascript
   const element = document.getElementById("myElementId");
   element.textContent = "New Text Content";
   ```

### Changing Styles

1. **style property**

   ```javascript
   const element = document.getElementById("myElementId");
   element.style.color = "red";
   element.style.backgroundColor = "yellow";
   ```

2. **classList property**
   ```javascript
   const element = document.getElementById("myElementId");
   element.classList.add("newClass"); // Add a class
   element.classList.remove("oldClass"); // Remove a class
   element.classList.toggle("toggleClass"); // Toggle a class
   ```

### Adding and Removing Elements

1. **createElement**

   ```javascript
   const newElement = document.createElement("div");
   newElement.textContent = "I am a new element";
   document.body.appendChild(newElement); // Add the new element to the body
   ```

2. **removeChild**

   ```javascript
   const parentElement = document.getElementById("parentElementId");
   const childElement = document.getElementById("childElementId");
   parentElement.removeChild(childElement); // Remove the child element from the parent
   ```

3. **insertBefore**

   ```javascript
   const newElement = document.createElement("div");
   newElement.textContent = "I am a new element";

   const parentElement = document.getElementById("parentElementId");
   const referenceElement = document.getElementById("referenceElementId");

   parentElement.insertBefore(newElement, referenceElement); // Insert the new element before the reference element
   ```

### Event Handling

1. **addEventListener**

   ```javascript
   const button = document.getElementById("myButton");
   button.addEventListener("click", () => {
     alert("Button was clicked!");
   });
   ```

2. **removeEventListener**

   ```javascript
   const button = document.getElementById("myButton");
   const handleClick = () => {
     alert("Button was clicked!");
   };

   button.addEventListener("click", handleClick);
   button.removeEventListener("click", handleClick);
   ```

### Example: Dynamic Content Update

Here’s a full example demonstrating several DOM manipulation techniques:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>DOM Manipulation Example</title>
  </head>
  <body>
    <div id="content">
      <p class="text">Original Text</p>
    </div>
    <button id="updateButton">Update Content</button>

    <script>
      document.getElementById("updateButton").addEventListener("click", () => {
        // Select the element
        const contentDiv = document.getElementById("content");
        const textElement = contentDiv.querySelector(".text");

        // Change the text content
        textElement.textContent = "Updated Text";

        // Change the style
        textElement.style.color = "blue";

        // Add a new element
        const newElement = document.createElement("p");
        newElement.textContent = "This is a new paragraph";
        contentDiv.appendChild(newElement);
      });
    </script>
  </body>
</html>
```

In this example:

- A button click triggers an event listener.
- The text content of an existing element is updated.
- The style of the element is changed.
- A new element is created and appended to the DOM.

### Simplified representation of the DOM structure using a JavaScript object notation

```js
const document = {
  documentElement: {
    nodeName: "HTML",
    children: [
      {
        nodeName: "HEAD",
        children: [
          {
            nodeName: "TITLE",
            textContent: "Document Title",
            children: [],
          },
        ],
      },
      {
        nodeName: "BODY",
        children: [
          {
            nodeName: "HEADER",
            children: [
              {
                nodeName: "H1",
                textContent: "Page Title",
                children: [],
              },
            ],
          },
          {
            nodeName: "MAIN",
            children: [
              {
                nodeName: "P",
                textContent: "This is a paragraph.",
                children: [],
              },
            ],
          },
          {
            nodeName: "FOOTER",
            children: [
              {
                nodeName: "P",
                textContent: "Footer content",
                children: [],
              },
            ],
          },
        ],
      },
    ],
  },
  head: {
    nodeName: "HEAD",
    children: [
      {
        nodeName: "TITLE",
        textContent: "Document Title",
        children: [],
      },
    ],
  },
  body: {
    nodeName: "BODY",
    children: [
      {
        nodeName: "HEADER",
        children: [
          {
            nodeName: "H1",
            textContent: "Page Title",
            children: [],
          },
        ],
      },
      {
        nodeName: "MAIN",
        children: [
          {
            nodeName: "P",
            textContent: "This is a paragraph.",
            children: [],
          },
        ],
      },
      {
        nodeName: "FOOTER",
        children: [
          {
            nodeName: "P",
            textContent: "Footer content",
            children: [],
          },
        ],
      },
    ],
  },
};

// Accessing elements
console.log(document.head.children[0].textContent); // Output: Document Title
console.log(document.body.children[0].children[0].textContent); // Output: Page Title
console.log(document.body.children[1].children[0].textContent); // Output: This is a paragraph.
console.log(document.body.children[2].children[0].textContent); // Output: Footer content
```

### Summary

- **Selecting Elements:** Methods include `getElementById`, `getElementsByClassName`, `getElementsByTagName`, `querySelector`, and `querySelectorAll`.
- **Changing Content:** Use `innerHTML` or `textContent`.
- **Changing Styles:** Use the `style` property or `classList`.
- **Adding and Removing Elements:** Use `createElement`, `appendChild`, `removeChild`, and `insertBefore`.
- **Event Handling:** Use `addEventListener` and `removeEventListener`.
