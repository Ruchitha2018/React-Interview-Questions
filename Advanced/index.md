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

## How do you access imperative API of web components?
