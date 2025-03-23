## What is Reselect Library?
- Reselect is a selector library for Redux that helps optimize derived state calculations.
- Improves Performance – Memoizes selectors to avoid unnecessary re-computation.
- Works with Redux State – Extracts and derives data efficiently.
- Composes Selectors – Allows chaining multiple selectors.

## Do you need to have a particular build tool to use Redux?
No, you don’t need a specific build tool to use Redux. Redux can be used with plain JavaScript, but in modern projects, it's often bundled with tools like Webpack, Vite, or Parcel for better development and performance optimization.

## What is Render Hijacking?

## What is the purpose of registerServiceWorker in React?
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

- Works only on https:// or localhost.
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