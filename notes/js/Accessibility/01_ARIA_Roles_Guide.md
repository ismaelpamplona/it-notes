# ARIA (Accessible Rich Internet Applications) Roles

ARIA (Accessible Rich Internet Applications) is a set of attributes that define ways to make web content and web applications more accessible to people with disabilities. These attributes provide additional information to screen readers and other assistive technologies about the roles, states, and properties of elements.

## ARIA Roles

### Landmark Roles

Landmark roles help users navigate web content by defining areas of a page.

- **banner**: Represents site-oriented content at the beginning of each page within a site.

  ```html
  <header role="banner">Site Header</header>
  ```

- **navigation**: Represents a section of the page intended for navigation.

  ```html
  <nav role="navigation">Main Navigation</nav>
  ```

- **main**: Represents the main content of a document.

  ```html
  <main role="main">Main Content</main>
  ```

- **complementary**: Represents a supporting section of the document.

  ```html
  <aside role="complementary">Related Content</aside>
  ```

- **contentinfo**: Represents site-oriented content at the end of the page.
  ```html
  <footer role="contentinfo">Site Footer</footer>
  ```

### Document Structure Roles

These roles define the structure of a document.

- **article**: Represents a self-contained composition in a document.

  ```html
  <article role="article">Article Content</article>
  ```

- **section**: Represents a generic section of a document.

  ```html
  <section role="region">Section Content</section>
  ```

- **heading**: Represents a heading for a section of the document.

  ```html
  <h1 role="heading" aria-level="1">Heading Level 1</h1>
  ```

- **list**: Represents a list of items.

  ```html
  <ul role="list">
    List Items
  </ul>
  ```

- **listitem**: Represents a single item in a list.
  ```html
  <li role="listitem">List Item</li>
  ```

### Widget Roles

Widget roles define interactive controls.

- **button**: Represents a clickable button.

  ```html
  <button role="button">Click Me</button>
  ```

- **checkbox**: Represents a checkbox that can be checked, unchecked, or mixed.

  ```html
  <input type="checkbox" role="checkbox" />
  ```

- **textbox**: Represents an input field where the user can enter text.

  ```html
  <input type="text" role="textbox" />
  ```

- **slider**: Represents a control for selecting a value from a range.

  ```html
  <input type="range" role="slider" />
  ```

- **menu**: Represents a menu of commands or options.

  ```html
  <ul role="menu">
    <li role="menuitem">Option 1</li>
    <li role="menuitem">Option 2</li>
  </ul>
  ```

- **tab**: Represents a tab in a tabbed interface.

  ```html
  <div role="tablist">
    <button role="tab">Tab 1</button>
    <button role="tab">Tab 2</button>
  </div>
  ```

- **tabpanel**: Represents the content associated with a tab.
  ```html
  <div role="tabpanel">Tab 1 Content</div>
  <div role="tabpanel">Tab 2 Content</div>
  ```

### Live Region Roles

Live region roles provide information about changes to sections of a page that may be dynamically updated.

- **alert**: Represents a message with important, and usually time-sensitive, information.

  ```html
  <div role="alert">This is an alert message.</div>
  ```

- **status**: Represents a status message providing information about the result of an action.
  ```html
  <div role="status">Status message here.</div>
  ```

### ARIA Attributes

ARIA attributes provide additional information about roles.

- **aria-labelledby**: Identifies the element that labels the current element.

  ```html
  <input type="text" aria-labelledby="label1" /> <label id="label1">Name</label>
  ```

- **aria-describedby**: Identifies the element that describes the current element.

  ```html
  <input type="text" aria-describedby="desc1" />
  <div id="desc1">Enter your full name.</div>
  ```

- **aria-checked**: Indicates the current "checked" state of checkboxes, radio buttons, and other widgets.

  ```html
  <input type="checkbox" aria-checked="false" />
  ```

- **aria-expanded**: Indicates whether an expandable section of the page is currently expanded or collapsed.
  ```html
  <button aria-expanded="false">Show More</button>
  ```

### Summary

ARIA roles, states, and properties enhance accessibility by providing additional information to assistive technologies. Implementing ARIA best practices ensures that web content is more accessible to users with disabilities.
