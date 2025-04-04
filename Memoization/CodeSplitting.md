# Code-Splitting
- Code-splitting is a technique that splits the JavaScript bundle into smaller chunks, loading only what is needed. This improves performance by reducing initial load time.

## Why Code-Splitting?
- Reduces initial bundle size
- Improves page load speed
- Loads only necessary code when needed

## How to implement?
### 1. Using `React.lazy` & `Suspense` (For Components)

```js
import React, { Suspense, lazy } from "react";

const LazyComponent = lazy(() => import("./MyComponent"));

const App = () => (
  <Suspense fallback={<div>Loading...</div>}>
    <LazyComponent />
  </Suspense>
);

export default App;
```

### 2. Using Dynamic Imports (For Modules)
```js
import("./utils").then((module) => {
  module.someFunction();
});
```

### 3. Code-Splitting with React Router (For Pages)
```js
//Each route loads only when accessed, reducing initial load time.
import { BrowserRouter as Router, Routes, Route } from "react-router-dom";
import { Suspense, lazy } from "react";

const Home = lazy(() => import("./Home"));
const About = lazy(() => import("./About"));

const App = () => (
  <Router>
    <Suspense fallback={<div>Loading...</div>}>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </Suspense>
  </Router>
);

export default App;
```
### 4. Webpack Configuration for Code-Splitting
```js
module.exports = {
  entry: {
    main: "./src/index.js",
  },
  output: {
    filename: "[name].[contenthash].js", // Generates unique names for cache busting
    path: __dirname + "/dist",
  },
  optimization: {
    splitChunks: {
      chunks: "all", // Splits both dynamic & static imports
    },
  },
};
```
- This automatically splits vendor libraries (`react`, `lodash`, etc.) into separate bundles.

## What are loadable components?
- React has built-in lazy loading via `React.lazy` and `Suspense`, but it doesn't support:
  - Server-side rendering (SSR)
  - Named exports
  - Better control over loading and fallback
  - Prefetching available
  - More suited for production and larger apps

```js
npm install @loadable/component
```
```js
import loadable from '@loadable/component';

// Dynamically import a component
const About = loadable(() => import('./About'));

function App() {
  return (
    <div>
      <h1>Welcome</h1>
      <About />
    </div>
  );
}
```
```js
const About = loadable(() => import('./About'), {
  fallback: <div>Loading...</div>,
});
```