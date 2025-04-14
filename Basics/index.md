# Basics

## 1. What is React?

- Open-Source
- JS Frontend Library
- Used for building composable UIs particularly for SPAs.
  
## 2. What are the features of React?
- Uses JSX Syntax: A syntax extension that allows you to write HTML-like code within JavaScript.
- Uses Virtual DOM
- Component Based Architecture
- Supports Server Side Rendering using Next.js, which is useful for SEO.
- Unidirectional/one-way data flow


## 3. What is JSX?

- A syntax extension that allows you to write HTML-like code within JavaScript.
- Syntactic Sugar for the `React.createElement(type, props, ...children)`

## 4. What are the ways of creating components

- Functional Components
- Class Components

## 5. What are States?

- It is an object that is used to store information and holds dynamic data while the app is running, like user input, button clicks, or data fetched from a server.
- Mutuable and Dynamic Data
- When a components state changes, React automatically re-renders
- Managed with `useState` hook.

## 6. What are Props?

- Way to pass static/dynamic data from parent to child components.
- Immutable
- Passed as Attributes

## 7. What is Key Prop?

- Special attribute should include when mapping arrays/objects.
- Helps which items have changed, added or removed.
- Used for performance optimization.
- Should be unique value

## 8. What is Virtual DOM?

- It is the lightweight copy of the real DOM.
- Steps:
  - When component re-renders, React creates a virtual copy of the Real DOM i.e., virtual DOM.
  - When app data changes, React first updates the Virtual DOM, not the Real DOM.
  - React compares the updated virtual DOM with the previous version of the virtual DOM called **Diffing**.
  - React identifies which parts of the virtual DOM have changed (e.g., new elements, deleted elements, updated content) and needs to be reflected in the real DOM.
  - It updates only the changed parts of the real DOM, making the app fast and efficient called **Reconciliation**.
  - Reconciliation helps React figure out the smallest number of changes to make, improving performance and speed.
  - 
## 9. What are Controlled Components?

- Forms element state is managed by React.
- Value of the input is controlled by the components state.
- Uses `useState()`

## 10. What are Uncontrolled Components?

- Forms element state is managed by DOM.
- Input value is accessed using a ```ref```.

## 11. What is React Fiber
- React Fiber is the new reconciliation engine in React (introduced in React 16) that improves rendering performance.
  - Incremental rendering – Splits work into chunks for smooth updates
  - Concurrency – Prioritizes updates for a better user experience
  - Pausing & resuming rendering – Avoids UI blocking
  - Better animations & transitions – More fluid interactions

## 12. What are Synthetic Events?
- Are wrapper elements around the browser's native element.
- Provide consistent behaviour across different browsers and optimize event handling.

## 13. What is Children Prop?
- It is a special prop that allows to pass content(text, element or component) to a component from its parent.
- commonly used in layout components like wrappers, containers or modal dialogs.

## 14. What are Fragments?

- It is the way to group multiple elements together without adding extra `div` or nodes.
- `<></>`
- `<React.Fragment></React.Fragment>`

## 15. What are Portals?

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
## 16. How to apply validation on props in React?
1. Using PropTypes (for JavaScript)
```js
npm install prop-types
```
```js
import React from "react";
import PropTypes from "prop-types";

const MyComponent = ({ name, age, isAdmin }) => {
  return (
    <div>
      <h2>Name: {name}</h2>
      <p>Age: {age}</p>
      <p>{isAdmin ? "Admin" : "User"}</p>
    </div>
  );
};

// Define prop types and make some required
MyComponent.propTypes = {
  name: PropTypes.string.isRequired, // Required string
  age: PropTypes.number, // Optional number
  isAdmin: PropTypes.bool, // Boolean
};

export default MyComponent;
```
2. Using TypeScript
   - TypeScript ensures type safety at compile time, preventing invalid props from being passed.
x
```js
import React from "react";
import PropTypes from "prop-types";

const MyComponent = ({ name, age, isAdmin }) => {
  return (
    <div>
      <h2>Name: {name}</h2>
      <p>Age: {age}</p>
      <p>{isAdmin ? "Admin" : "User"}</p>
    </div>
  );
};

// Define prop types and make some required
MyComponent.propTypes = {
  name: PropTypes.string.isRequired, // Required string
  age: PropTypes.number, // Optional number
  isAdmin: PropTypes.bool, // Boolean
};

export default MyComponent;
```
| Feature           | PropTypes       | TypeScript     |
|------------------|---------------|---------------|
| **Validation**   | Runtime        | Compile-time  |
| **Error Detection** | Console warnings | Build-time errors |
| **Performance**  | Slightly slower | Faster        |
| **Additional Setup** | Install `prop-types` | Use `.tsx` file |

## 17. What are the limitations of React?

|  **Limitation**                            | **Solution**                                                                 |
|---------------------------------------------|----------------------------------------------------------------------------------|
| **1. SEO Limitations**                      | Use **Next.js** or **Remix** for SSR/SSG; use `react-helmet` for meta tags      |
| **2. High Initial Load Time**               | Use **Code Splitting** (`React.lazy`, `Suspense`); optimize bundle size         |
| **3. Boilerplate Code & Verbosity**         | Use frameworks like **Next.js**; use **Redux Toolkit** or **Context API**       |
| **4. State Management for Large Apps**      | Use **Redux**, **Recoil**, or **Zustand**; use **Formik** or **React Hook Form**|
| **5. Performance Issues (Re-rendering)**    | Use `React.memo`, `useMemo`, `useCallback`; use **React Profiler**              |
| **6. Steep Learning Curve**                 | Follow a structured learning path; use **React Dev Tools** for easier debugging |
| **7. No Built-in Routing or Forms**         | Use **React Router**, **React Hook Form**, **React Query / SWR**                |



## 18. Difference between React and React DOM:
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

## 19. Why we need to be careful when spreading props on DOM elements?
1. Unintended Props – Extra or invalid props may get added, causing React warnings.
```js
const Button = (props) => <button {...props}>Click</button>;
<Button color="blue" onClick={() => alert("Clicked!")} />;
```
2. Performance Issues – Passing unnecessary props can lead to extra re-renders.
3. Security Risks – If props come from untrusted sources, it may lead to XSS vulnerabilities.
```js
const userProps = { onClick: () => alert("Clicked!"), dangerous: "<script>alert('XSS')</script>" };
<div {...userProps} />;
```
4. Loss of Control – Harder to track which props are being passed, making debugging difficult.
5. Invalid HTML Attributes – Non-standard attributes may end up in the DOM, affecting behavior.
6. **Best Practice:** Filter and pass only required props instead of using `{...props}` blindly. 

## 20. What is Switching Component?
A switching component in React is a component that conditionally renders different components based on a specific condition (like state, props, or routes).
 #### Example 1: Conditional Rendering (Manual Switching)
 ```js
 const SwitchingComponent = ({ userType }) => {
  if (userType === "admin") {
    return <AdminPanel />;
  } else if (userType === "user") {
    return <UserDashboard />;
  } else {
    return <GuestPage />;
  }
};

// Usage
<SwitchingComponent userType="admin" />;
```
#### Example 2: Using React Router (Route Switching)
```js
import { BrowserRouter as Router, Routes, Route } from "react-router-dom";
import Home from "./Home";
import About from "./About";
import NotFound from "./NotFound";

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="*" element={<NotFound />} />  {/* Default fallback */}
      </Routes>
    </Router>
  );
};
```

## 21. What are React Mixins?
- Mixins were a feature in React class components (before ES6 classes) that allowed **sharing reusable logic** across multiple components. 
- Removed in React 16 due to:
  - Name Collisions – Multiple mixins could have the same method names, causing conflicts.
  - Implicit Dependencies – Hard to track where a method came from.
  - Performance Issues – Mixins led to unpredictable re-renders.
  - Harder to Maintain – Code became difficult to debug as mixins spread logic across components.
- Replaced by better alternatives like:
  - Higher-Order Components (HOCs) – Wraps a component to add functionality.
  - Custom Hooks (Recommended) – Encapsulates reusable logic in function components.
- Modern React (with Hooks) does not support Mixins.


## 22. What are React Components Naming?

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

## 23. Are custom DOM attributes supported in React v16?
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

## 24. Why we cant use for loop inside jsx?
- You can't use a for loop directly inside JSX because JSX expects expressions, and for is a statement, not an expression.
- Expressions return values, statements perform actions!

## 25. Why you can't update props in React?
- Props are immutable: They cannot be changed by the child component.
- Unidirectional data flow: Props flow from parent to child, ensuring predictable updates.
- Controlled by parent: Props reflect parent state; only the parent can update them.
- Solution: Manage the value in the parent’s state and pass it via props.
## 26. What are the React Animation Packages?
- Framer Motion
- React Spring
- React Transition Group
- React Motion

## 27. What are React Specific Linters?
- Help maintain clean, consistent and error-free code in React Projects.
- Plugins:
 - ```eslint-plugin-react```: Provides linting rules for React.
 - ```eslint-plugin-react-hooks```: Ensures the correct usage of React Hooks.
 - ```eslint-plugin-jsx-a11y```: Enforces accessibility best practices in JSX code.
 - Code formatter, integrates with ESLint using ```eslint-plugin-prettier```.

## 28. How events are different in React?
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

## 29. What is the impact of indexes as keys?
- Re-renders Unnecessary Components – If the list order changes, React mistakenly reuses incorrect components.
- Loss of State – Input fields, animations, or user interactions reset unexpectedly.
- Performance Issues – React does extra work re-rendering items when not needed.
- Breaks Component Identity – Moves components incorrectly when items are added/removed.
-  Only use indexes when the list is static and never reorders!