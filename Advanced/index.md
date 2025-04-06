# Advanced

## What is Reselect Library?
- Reselect is a selector library for Redux that helps optimize derived state selection by memoizing computed values.
- Improves Performance – Memoizes selectors to avoid unnecessary re-computation.
- Works with Redux State – Extracts and derives data efficiently.
- Composes Selectors – Allows chaining multiple selectors.

```js
//Example without Reselect
const getUsers = (state) => state.users;
const getFilter = (state) => state.filter;

// Non-memoized selector (Recomputes every time)
const getFilteredUsers = (state) => {
  console.log("Recalculating filtered users...");
  return state.users.filter(user => user.name.includes(state.filter));
};

// Redux state
const state = {
  users: [{ name: "Alice" }, { name: "Bob" }],
  filter: "A"
};

// Each call recalculates the filtered users
console.log(getFilteredUsers(state)); // [{ name: "Alice" }]
console.log(getFilteredUsers(state)); // Recomputes every time
```

```js
//Example with Reselect
import { createSelector } from 'reselect';

const getUsers = (state) => state.users;
const getFilter = (state) => state.filter;

// Memoized Selector
const getFilteredUsers = createSelector(
  [getUsers, getFilter],
  (users, filter) => {
    console.log("Recalculating filtered users...");
    return users.filter(user => user.name.includes(filter));
  }
);

// Redux state
console.log(getFilteredUsers(state)); // [{ name: "Alice" }] (Recalculates)
console.log(getFilteredUsers(state)); // Uses cached result (No recalculation)
```
---
## Do you need to have a particular build tool to use Redux?
No, you don’t need a specific build tool to use Redux. Redux can be used with plain JavaScript, but in modern projects, it's often bundled with tools like Webpack, Vite, or Parcel for better development and performance optimization.

## What is Render Hijacking?

## What is the purpose of `registerServiceWorker` in React?
1. Offline Support: Allows the app to work without an internet connection by caching files.
2. Faster Loading: Loads the app faster by using cached assets instead of fetching them from the network.
3. Background Features: Enables tasks like background sync and push notifications.
4. Progressive Web Apps (PWA): Helps turn your app into a PWA with app-like features.

```js
import * as serviceWorker from './serviceWorker';

// Enable service worker for offline support
serviceWorker.register(); // Registers the service worker
// Use serviceWorker.unregister() if you don't need it.
```

- Works only on `https://` or `localhost`.
- Use carefully to avoid serving outdated cached content.

## Flux vs Redux

## Error Boundaries

## What is the purpose of `displayName` class property?
 - Purpose: Helps in debugging by assigning a custom name to a component.
- Used in: Functional & Class components, Higher-Order Components (HOCs).
- Improves: Readability in React DevTools.

```js
const Greeting = ({ name }) => <h2>Hello, {name}!</h2>;
Greeting.displayName = "CustomGreeting";  
export default Greeting;
```
-  Now, DevTools will show `CustomGreeting`
## What is the browser support for react applications?
- React applications work on all modern browsers that support ES6+ and JSX.
- Not Supported (without polyfills)
  - Internet Explorer (IE 11 and older) (React dropped support in v18)
#### How to Support Older Browsers?
- Use Babel – Transpiles ES6+ code into ES5 for older browsers.
- Polyfills – Add features like `fetch`, `Promise`, and `Object.assign`.
- `npm install core-js regenerator-runtime`
```js
import "core-js/stable";
import "regenerator-runtime/runtime";
```
---
## What is Keyed Fragments?
- A fragment in React `(<></>)` lets you group multiple elements without adding extra nodes to the DOM. Sometimes, when you map over a list and return fragments, you need to assign a unique key to each one — that’s when you use keyed fragments.

```js
const items = [
  { id: 1, title: 'One', description: 'First item' },
  { id: 2, title: 'Two', description: 'Second item' },
];

function ItemList() {
  return (
    <div>
      {items.map((item) => (
        <React.Fragment key={item.id}>
          <h2>{item.title}</h2>
          <p>{item.description}</p>
        </React.Fragment>
      ))}
    </div>
  );
}
```
```js
{items.map((item) => (
  <>  {/* ❌ Can't put key here */}
    <h2>{item.title}</h2>
    <p>{item.description}</p>
  </>
))}
```

## Does React support all HTML attributes?
1. Common attributes like `src`, `alt`, `href`, `type`, `value`, etc., work as expected.
2. Some attribute names are different (camelCase).
   - `class` → `className`
   - `for` → `htmlFor`
   - `readonly` → `readOnly`
   - `maxlength` → `maxLength`
3. Events use camelCase.
   - `onclick` → `onClick`
   - `onchange` → `onChange`
4. Form elements are controlled using state.
```js
<input value={text} onChange={handleChange} />
```
5. Some attributes need special handling.
- Use `autoFocus`, `dangerouslySetInnerHTML`, etc.

## How JSX prevents Injection Attacks?
### 1. JSX Escapes Content Automatically

- Any value inside `{}` in JSX is **escaped by default**.
- Special characters (`<`, `>`, `"`, `'`, `/`) are converted to **safe strings**.

**Example:**
```jsx
const input = "<script>alert('Hacked!')</script>";
<p>{input}</p> // Renders as: &lt;script&gt;alert('Hacked!')&lt;/script&gt;
```
- Nothing dangerous will run — it's shown as plain text.

---

### 2. Prevents HTML or Script Injection

- JSX does **not run** any HTML or JavaScript inserted via strings.
- Protects your app from **Cross-Site Scripting (XSS)** attacks.

---

### 3. React Sanitizes All Interpolated Content

- Values inside JSX `{}` are **sanitized**.
- Dangerous user input will not affect the DOM.

**Example:**
```jsx
<input value={userInput} /> // Safe
```

---

### 4. Only `dangerouslySetInnerHTML` Can Inject Raw HTML

- Use **only with trusted or sanitized data**.

**Example:**
```jsx
<div dangerouslySetInnerHTML={{ __html: "<b>Bold</b>" }} />
```
⚠️ Unsafe if you use raw user input — can lead to XSS.

---

### 5. JSX Never Executes JavaScript Strings

- Code like `alert("hi")` is treated as a **string**, not as code.

**Example:**
```jsx
const input = "alert('hi')";
<p>{input}</p> // Just prints alert('hi')
```

---

### 6. Safe by Default — Unless You Bypass It

- Without `dangerouslySetInnerHTML`, JSX is secure.
- No need to sanitize most content manually.

---
## When do you need to use refs?
- Managing focus, text selection, or media playback
```js
const inputRef = useRef();

useEffect(() => {
  inputRef.current.focus();
}, []);
```
- Triggering animations or transitions manually
```js
const boxRef = useRef();

useEffect(() => {
  gsap.to(boxRef.current, { x: 100 });
}, []);
```
- Measuring element dimensions/position (e.g., height, offset)
```js
const divRef = useRef();

useEffect(() => {
  console.log(divRef.current.offsetHeight);
}, []);
```
- Accessing child component methods (only for class components or forwardRef components)
```js
// Child.jsx
import React, { useImperativeHandle, forwardRef, useRef } from 'react';

const Child = forwardRef((props, ref) => {
  const inputRef = useRef();

  // Expose methods to parent via the ref
  useImperativeHandle(ref, () => ({
    focusInput: () => {
      inputRef.current.focus();
    },
    sayHi: () => alert('Hi from Child!')
  }));

  return <input ref={inputRef} placeholder="Type here" />;
});

export default Child;
```
```js
// Parent.jsx
import React, { useRef, useEffect } from 'react';
import Child from './Child';

function Parent() {
  const childRef = useRef();

  useEffect(() => {
    childRef.current.focusInput();
    childRef.current.sayHi();
  }, []);

  return <Child ref={childRef} />;
}
```
- Preserving values across renders (without causing re-renders)
```js
const renderCount = useRef(0);
renderCount.current += 1;
```
## What is windowing technique?
- The windowing technique (also known as virtualization) is a performance optimization strategy in frontend development — especially useful when rendering large lists or tables in the UI.
- The windowing technique renders only the items currently visible in the viewport (plus a few extra for smoother scrolling). As the user scrolls, items are recycled and updated to reflect new content.
- Improves performance
- Reduces memory usage
- Speeds up rendering
- When to use it?
  - Large lists (e.g., 1000+ items)
  - Tables with lots of rows
  - Infinite scroll UIs
- Libraries
  - `react-window` (lightweight, by Brian Vaughn)
  - `react-virtualized` (more powerful but heavier)
  - `TanStack Virtual` (framework-agnostic, modern)
- Real-World Use Cases
  - Long dropdowns
  - Chat apps
  - Log viewers
  - Search results
  - Data-heavy dashboards

## Can you list down top websites or applications using react as front end framework?
1. Tech Giants & Social Media
  - Facebook – Developed React and uses it extensively.
  - Instagram – Uses React for web UI components.
  - WhatsApp Web – Built using React.
  - Twitter (New Web App) – Uses React for a modern UI.
  - Reddit – The latest web version is built with React.

2. E-Commerce & Payments
Amazon (AWS Amplify UI) – Uses React in AWS services.

Netflix – React improves load speeds and performance.

Walmart – Uses React for a better user experience.

Shopify – Storefronts and dashboards use React.

PayPal – React is part of their web application stack.

3. Productivity & Collaboration Tools
Dropbox – Uses React for file management UI.

Trello – Kanban-based project management tool powered by React.

Asana – Uses React for task and project management.

Notion – Uses React for note-taking and database UI.

Microsoft Office Web Apps – Word, Excel, etc., use React.

4. Streaming & Entertainment
Spotify – Web-based music player built with React.

YouTube TV – Uses React in its TV interface.

Hulu – React enhances their UI experience.

5. Development & Learning Platforms
GitHub – Some UI parts, including GitHub Desktop, use React.

CodeSandbox – Online React-based code editor.

Coursera – Uses React for online courses.

Udemy – Uses React in its learning platform.

6. Other Notable Mentions
Airbnb – Uses React for booking UI.

Uber – React powers the web app and dashboard.

Tesla – Uses React for web and control panel interfaces.

## Why do we use array destructuring (square brackets notation) in `useState`?

## Why Were Hooks Introduced?
- Eliminate Class Component Complexity – No need for this, binding, and lifecycle confusion.
- Improve Code Reusability – Custom hooks allow logic sharing across components.
- Better State Management – useState, useEffect, useReducer simplify state handling.
- Enhance Performance – Hooks optimize re-renders by managing dependencies effectively.

## What is an Imperative API?
An Imperative API allows direct control over an object/component using methods. It tells how to do something.
- Direct Commands – You explicitly call functions/methods.
- Immediate Execution – Runs instructions step-by-step.
- Mutates State Directly – Doesn't rely on declarative updates.
```js
//Imperative Approach
function MyComponent() {
  const inputRef = useRef(null);

  const focusInput = () => {
    inputRef.current.focus(); // Directly calling a method
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}
```
```js
//Declarative Approach
function MyComponent() {
  const [isFocused, setIsFocused] = useState(false);

  return (
    <div>
      <input autoFocus={isFocused} type="text" />
      <button onClick={() => setIsFocused(true)}>Focus Input</button>
    </div>
  );
}
```
### Examples
- DOM Methods – focus(), scrollTo(), play()
- Web Component Methods – Custom elements exposing .open(), .close(), etc.
- Canvas API – ctx.fillRect(), ctx.drawImage()
- Third-Party Libraries – Modals (modal.show()), Maps (map.setCenter())

### When to use?
- When interacting with the DOM (e.g., focusing an input).
- When using third-party libraries that rely on methods.
- When performance optimization is needed (e.g., avoiding unnecessary re-renders).

## How do you access imperative API of web components?
- Use `useRef` – To get a reference to the Web Component.
- Use `useEffect` – To interact with the component after it mounts.
- Directly call methods – Access Web Component methods via `ref.current`.

```js
<script>
  class CustomButton extends HTMLElement {
    connectedCallback() {
      this.innerHTML = `<button>Click Me</button>`;
    }

    focusButton() {
      this.querySelector("button").focus();
    }
  }
  customElements.define("custom-button", CustomButton);
</script>
```
```js
import { useEffect, useRef } from "react";

function App() {
  const buttonRef = useRef(null);

  useEffect(() => {
    if (buttonRef.current) {
      buttonRef.current.focusButton(); // Calling the Web Component's method
    }
  }, []);

  return <custom-button ref={buttonRef}></custom-button>;
}

export default App;
```
## Do browsers understand JSX code?
Browsers do not natively understand JSX, but tools like Babel convert it into JavaScript that browsers can execute.

## Describe about data flow in react?
- Unidirectional Data Flow → Ensures predictable state updates.
- Props for Parent-to-Child → Best for passing read-only data.
- Callbacks for Child-to-Parent → Used for event handling.
- State Lifting for Sibling Data Sharing → Common in form handling.
- Global State (Redux, Context API, Zustand, etc.) for Complex Apps → Used when many components need access to the same data.

## What is Concurrent Rendering?
- Concurrent Rendering is a React feature that allows rendering multiple UI tasks without blocking the main thread, making apps more responsive and smoother.
- Interruptible Rendering – React can pause and resume rendering when needed.
- Prioritization – High-priority updates (like user input) can be processed first.
- Background Rendering – Low-priority tasks run in the background without blocking the UI.

### APIs for Concurrent Rendering:
- useTransition() – Defers low-priority updates.
- useDeferredValue() – Delays value updates smoothly.
- Suspense – Loads components lazily without blocking UI.

### With Concurrent Rendering (Non-Blocking UI):
- React splits rendering into smaller chunks and prioritizes urgent updates.
- Introduced via React 18’s `createRoot()` API.

## How do you implement Server Side Rendering or SSR?
1. Create an Express Server (`server.js`)
```js
import express from "express";
import React from "react";
import ReactDOMServer from "react-dom/server";
import App from "./src/App"; // Import your React App component

const app = express();

app.use(express.static("build")); // Serve static files

app.get("*", (req, res) => {
  const appHTML = ReactDOMServer.renderToString(<App />);

  res.send(`
    <!DOCTYPE html>
    <html lang="en">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>React SSR</title>
    </head>
    <body>
      <div id="root">${appHTML}</div>
      <script src="/static/js/main.js"></script>
    </body>
    </html>
  `);
});

app.listen(3000, () => console.log("Server running on http://localhost:3000"));
```
2. Modify `index.js` (Hydrate on Client)
```js
import React from "react";
import { hydrateRoot } from "react-dom/client";
import App from "./App";

hydrateRoot(document.getElementById("root"), <App />);
```
- Now, React renders on the server first, then hydrates on the client! 
- `hydrateRoot` is used for hydrating a server-rendered React app on the client.
- It attaches event listeners to existing server-rendered HTML instead of re-rendering it.
- Faster than `createRoot` because it doesn't replace the existing DOM.

## How to enable production mode in React?
- For Vite:
  - Run: `npm run build`
  - Preview: `npm run preview`
- For Webpack:
  - Set mode: "production" in `webpack.config.js`
  - Run: `npm run build`

## How does React batch multiple state updates?
- Batching means grouping multiple state updates into a single re-render to optimize performance.
```js
const [count1, setCount1] = useState(0);
const [count2, setCount2] = useState(0);

const handleClick = () => {
  setCount1(prev => prev + 1);
  setCount2(prev => prev + 1);
};
```
- When `handleClick` is called:
  - React batches `setCount1` and `setCount2`
  - Triggers only one re-render, not two
- Before React 18, batching did not happen in:
  - `setTimeout`, `Promise.then`, `fetch`, etc.
- In React 18+, batching works everywhere!
---
## How do you update nested objects inside state?
```js
const [user, setUser] = useState({
  name: "Ruchitha",
  address: {
    city: "Nanded",
    pincode: 421503
  }
});
```
```js
//To update city inside address:
setUser(prevUser => ({
  ...prevUser,
  address: {
    ...prevUser.address,
    city: "Mumbai"
  }
}));
```
- React state should be immutable, we use the spread operator to create a new copy of the object or array at each level, avoiding direct mutation.
---
## How do you update arrays inside state?

```js
const [fruits, setFruits] = useState(["apple", "banana", "orange"]);
```
```js
//Add an Item
setFruits(prevFruits => [...prevFruits, "mango"]);
```
```js
//Remove an Item
setFruits(prevFruits => prevFruits.filter(fruit => fruit !== "banana"));
```
```js
//Update an Item
setFruits(prevFruits =>
  prevFruits.map(fruit => fruit === "orange" ? "grape" : fruit)
);
```