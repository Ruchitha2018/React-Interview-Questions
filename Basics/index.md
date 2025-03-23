# Basics

## What is React?

- Open-Source
- JS Frontend Library
- used for building composable UIs particularly for SPAs.

## Features of React?

- Uses JSX Syntax: A syntax extension that allows you to write HTML-like code within JavaScript.
- Uses Virtual DOM
- Component Based Architecture
- Supports Server Side Rendering using Next.js, which is useful for SEO.
- Unidirectional/one-way data flow

## JSX

- A syntax extension that allows you to write HTML-like code within JavaScript.
- Syntactic Sugar for the `React.createElement(type, props, ...children)`

## Ways of creating components

- Functional Components
- Class Components

## What are States?

- It is an object that is used to store information and holds dynamic data while the app is running, like user input, button clicks, or data fetched from a server.
- Mutuable and Dynamic Data
- When a components state changes, React automatically re-renders
- Managed with `useState` hook.

## What are Props?

- Way to pass static/dynamic data from parent to child components.
- Immutable
- Passed as Attributes

## Key Prop?

- Special attribute should include when mapping arrays/objects.
- Helps which items have changed, added or removed.
- Used for performance optimization.
- Should be unique value

## Virtual DOM

- It is the lightweight copy of the real DOM.
- Steps:
  - When component re-renders, React creates a virtual copy of the Real DOM i.e., virtual DOM.
  - When app data changes, React first updates the Virtual DOM, not the Real DOM.
  - React compares the updated virtual DOM with the previous version of the virtual DOM called Diffing.
  - React identifies which parts of the virtual DOM have changed (e.g., new elements, deleted elements, updated content) and needs to be reflected in the real DOM.
  - It updates only the changed parts of the real DOM, making the app fast and efficient called Reconciliation.
  - Reconciliation helps React figure out the smallest number of changes to make, improving performance and speed.

## Controlled Components

- Forms element state is managed by React.
- Value of the input is controlled by the components state.
- Uses `useState()`

## Uncontrolled Components

- Forms element state is managed by DOM.
- Input value is accessed using a ```ref```.

## React Fiber
- React Fiber is the new reconciliation engine in React (introduced in React 16) that improves rendering performance.
  - Incremental rendering – Splits work into chunks for smooth updates
  - Concurrency – Prioritizes updates for a better user experience
  - Pausing & resuming rendering – Avoids UI blocking
  - Better animations & transitions – More fluid interactions

## Synthetic Events
- Are wrapper elements around the browser's native element.
- Provide consistent behaviour across different browsers and optimize event handling.

## Children Prop
- It is a special prop that allows to pass content(text, element or component) to a component from its parent.
- commonly used in layout components like wrappers, containers or modal dialogs.

## Fragments

- It is the way to group multiple elements together without adding extra `div` or nodes.
- `<></>`
- `<React.Fragment></React.Fragment>`

## Portals

- It allows us to render components outside the parent component DOM hierarchy.
- Examples are Modals, Tooltips, Notifications

```html
<div id="root"></div> <!-- Normal app -->
<div id="modal-root"></div> <!-- Space for portals -->
```
```js
import React from "react";
import ReactDOM from "react-dom";

function Modal({ children }) {
  return ReactDOM.createPortal(
    <div className="modal">{children}</div>,
    document.getElementById("modal-root") // Teleport here
  );
}

function App() {
  return (
    <div>
      <h1>My App</h1>
      <Modal>I'm a modal!</Modal> {/* Rendered outside */}
    </div>
  );
}

export default App;
```

## Difference between React and React DOM:
- React:
  - Used to build UI components and manage their logic and state
  - Do not directly interact with the DOM.
  - Works in both browser & server (`Next.js`, `React Native`)
  - Eg:- ```useState``` and ```useEffect```
  

- React DOM:
  - Renders React components to the browser DOM
  - Used to update the browser DOM efficiently using React's Virtual DOM
  - Works only in the browser (DOM manipulation)
  - Eg:- ```ReactDOM.createRoot```  and ```ReactDOM.render```

- Separation allows React to work on different platforms (e.g., React Native).
- Keeps React lightweight and modular for easier maintenance.

## How to combine multiple inline style objects?

```js
const App = () => (
  <div style={{ ...baseStyle, ...extraStyle }}>Hello, React!</div>
);
```

```js
const isDarkMode = true;
const darkModeStyle = { backgroundColor: "black", color: "white" };
const lightModeStyle = { backgroundColor: "white", color: "black" };

const App = () => (
  <div style={{ ...baseStyle, ...(isDarkMode ? darkModeStyle : lightModeStyle) }}>
    Theme Example
  </div>
);
```

## Why you can't update props in React?
- Props are immutable: They cannot be changed by the child component.
- Unidirectional data flow: Props flow from parent to child, ensuring predictable updates.
- Controlled by parent: Props reflect parent state; only the parent can update them.
- Solution: Manage the value in the parent’s state and pass it via props.

## React Components Naming

1. **Start with a Capital Letter:** Components must use PascalCase (e.g., MyComponent). Lowercase names are treated as HTML tags.
2. **Avoid Reserved Keywords:** Don't use JavaScript or HTML reserved words like return or default.
3. **No Special Characters:** Names cannot include dashes, spaces, or special symbols.
4. **Dynamic Names Not Allowed:** Components can't be named using strings or variables.
5. **Export-Import Match:** For named exports, import names must match the export. Default exports can use any name.

```js
const DynamicComponent = "MyComponent";
<DynamicComponent />; // Error: React cannot dynamically resolve this

const My-Component = () => {}; // Syntax error
```

### Instead use below:-

```js
const DynamicComponent = MyComponent;
<DynamicComponent />;
```

## What are the React Animation Packages?
- Framer Motion
- React Spring
- React Transition Group
- React Motion

## What are React Specific Linters?
- Help maintain clean, consistent and error-free code in React Projects.
- Plugins:
 - ```eslint-plugin-react```: Provides linting rules for React.
 - ```eslint-plugin-react-hooks```: Ensures the correct usage of React Hooks.
 - ```eslint-plugin-jsx-a11y```: Enforces accessibility best practices in JSX code.
 - Code formatter, integrates with ESLint using ```eslint-plugin-prettier```.

## Switching Components

## React Mixins

## Are custom DOM attributes supported in React v16?
- React 16+ supports custom DOM attributes without needing `data-` or `aria-` prefixes. and passes them to the rendered HTML.
```js
//Example
  <div custom-attr="hello">Hello World</div>
```
```js
//Output
<div custom-attr="hello">Hello World</div>
```
- Best practice: Use `data-*` attributes for consistency

## Why we cant use for loop inside jsx?
- You can't use a for loop directly inside JSX because JSX expects expressions, and for is a statement, not an expression.
- Expressions return values, statements perform actions!

## How events are different in React?
- React wraps native events in a SyntheticEvent wrapper for cross-browser consistency.
```js
function handleClick(event) {
  console.log(event); // React SyntheticEvent
}
<button onClick={handleClick}>Click Me</button>;
```
- Event Names Use CamelCase
  - React: onClick, onChange, onKeyDown
  - HTML: onclick, onchange, onkeydown
- No `return false` to Prevent Default
  - Use `event.preventDefault()` instead.
- Works the same across all browsers due to the SyntheticEvent wrapper.

## What is the impact of indexes as keys?
- Re-renders Unnecessary Components – If the list order changes, React mistakenly reuses incorrect components.
- Loss of State – Input fields, animations, or user interactions reset unexpectedly.
- Performance Issues – React does extra work re-rendering items when not needed.
- Breaks Component Identity – Moves components incorrectly when items are added/removed.
-  Only use indexes when the list is static and never reorders!