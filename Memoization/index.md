# Memoization

1. What is memoization?
2. React.memo
3. useMemo hook
4. useCallback hook
5. React.lazy and Suspense

### Definition:

Memoization is a **performance optimization** technique where the result of a function is cached so that it doesn’t need to be recomputed for the same inputs.

### Purpose:

Improves performance by avoiding redundant computations.

### How it Works:

- Stores input-output pairs in a cache.
- On repeated inputs, returns the cached result instead of recalculating.

### Use Cases:

- React:
  Hooks like ```useMemo``` and ``useCallback`` for caching values or functions.

- Dynamic Programming:
  For solving problems like Fibonacci, knapsack, etc.

- API Responses:
  Caching API results to avoid duplicate network calls.

- Data Filtering/Sorting:
  Avoid recomputing when data hasn’t changed.

### Benefits:

- Saves computation time.
- Reduces system load.

### Drawbacks:

- Uses extra memory for caching.
- Cache management can add complexity.

```js
const memoizedAdd = () => {
  const cache = {};
  return (a, b) => {
    const key = `${a},${b}`;
    if (cache[key]) {
      console.log("Fetching from cache...");
      return cache[key];
    }
    console.log("Calculating...");
    const result = a + b;
    cache[key] = result;
    return result;
  };
};

const add = memoizedAdd();
console.log(add(1, 2)); // Calculating...
console.log(add(1, 2)); // Fetching from cache...
```

## React Hooks and Utilities for Memoization

### 1. `React.memo`

- Memoizes a functional component so it only re-renders when its props change.
- Improves performance by skipping re-renders for components that receive the same props.
- If the props remain the same between renders, the component is not re-rendered.
- If we are sending the function as props, then `React.memo` wont work.

```js
import React from 'react';

const Child = React.memo(({ count }) => {
    console.log("Child rendered");
    return <div>Count: {count}</div>;
});

function Parent() {
    const [count, setCount] = React.useState(0);
    const [otherState, setOtherState] = React.useState(false);

    return (
        <div>
            <Child count={count} />
            <button onClick={() => setCount(count + 1)}>Increment Count</button>
            <button onClick={() => setOtherState(!otherState)}>Toggle Other State</button>
        </div>
    );
}

export default Parent;

```
- Child will only re-render when the `count` prop changes.
- The Child component is wrapped with `React.memo`, which prevents re-renders unless its props change.
- `count` is the only prop passed to Child, and it does not change when `otherState` updates.
- Since `otherState` is not a prop of Child, the Child component remains unchanged, and React skips its re-render.
- We can customize the comparison logic using a second argument to `React.memo`.


```js
const MyComponent = React.memo(
  (props) => {
    return <div>{props.value}</div>;
  },
  (prevProps, nextProps) => prevProps.value === nextProps.value
);
```

### 2. ```useMemo```
- Memoizes the result of a computation and recalculates it only when dependencies change.
```js
import React, { useState, useMemo } from 'react';

function ExpensiveCalculation(num) {
    console.log("Calculating...");
    return num * 2;
}

function App() {
    const [number, setNumber] = useState(0);
    const [toggle, setToggle] = useState(false);

    const doubled = useMemo(() => ExpensiveCalculation(number), [number]);

    return (
        <div>
            <h1>Doubled Value: {doubled}</h1>
            <button onClick={() => setNumber(number + 1)}>Increment</button>
            <button onClick={() => setToggle(!toggle)}>Toggle</button>
        </div>
    );
}

export default App;

```

- `ExpensiveCalculation` is only called when number changes.
- Changing `toggle` does not trigger the expensive calculation.


### 3. ```useCallback``` 

`useCallback` is a React hook that memoizes a function definition so that it doesn’t get recreated unnecessarily during re-renders.

- Purpose:
  - Prevents the creation of a new function on every render.
  - Useful when passing functions as props to child components.
- How It Works:
  - Returns a cached version of the function unless its dependencies change.

```js
const memoizedFunction = useCallback(() => {
  // Function logic here
}, [dependencies]);
```

- Parameters:
  - Callback Function: The function to be cached.
  - Dependencies: Values that, when changed, recreate the function.


```js
import React, { useState, useCallback } from 'react';

const Button = React.memo(({ handleClick }) => {
  console.log('Button re-rendered');
  return <button onClick={handleClick}>Click Me</button>;
});

const App = () => {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount((prevCount) => prevCount + 1);
  }, []);

  return (
    <div>
      <p>Count: {count}</p>
      <Button handleClick={increment} />
    </div>
  );
};

export default App;
```

- How it Helps in This Example

  - Without `useCallback`:
    The increment function is recreated on every render, causing the `Button` to re-render unnecessarily.

  - With `useCallback`:
    The increment function is cached and does not trigger a re-render of `Button` unless its dependencies change.

### 4. `React.lazy` function

- Dynamically loads components for code-splitting, reducing the initial bundle size.
- Loads components only when they are rendered.
- It helps reduce the initial load time by splitting the app into smaller bundles and loading components only when needed.
- Improves performance by reducing the size of the initial JavaScript bundle.

```js
import React, { Suspense } from 'react';

const LazyComponent = React.lazy(() => import('./MyComponent')); //File name without extension

export default function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <LazyComponent />
    </Suspense>
  );
}
```

- How it works?
  - `React.lazy` takes a function that dynamically imports a component `(e.g., () => import('./MyComponent'))`.
  - The component is loaded when it’s rendered for the first time.
  - A `Suspense` component is required to handle the loading state.

## How to Use `React.memo` Effectively When Passing Functions as Props?
- In JavaScript, functions are reference types.
- When a parent component re-renders, even if the logic of the function doesn't change, a new function reference is created and passed down as a prop.
- `React.memo` detects this new reference and considers it a prop change, so it re-renders the child component.
- To prevent unnecessary re-renders, use `React.memo` with `useCallback` to memoize the function in the parent component. This ensures the function reference stays the same unless its dependencies change.

```js
import React, { useState, useCallback } from 'react';

const Parent = () => {
  const [count, setCount] = useState(0);

  // Memoize the function to prevent unnecessary re-renders
  const handleClick = useCallback(() => {
    console.log('Button clicked!');
  }, []);

  return (
    <>
      <button onClick={() => setCount(count + 1)}>Increment: {count}</button>
      <Child onClick={handleClick} />
    </>
  );
};

const Child = React.memo(({ onClick }) => {
  console.log('Child re-rendered');
  return <button onClick={onClick}>Click Me</button>;
});
```

## How to Use `React.memo` Effectively When Passing Objects and Arrays as Props?
- When a parent component re-renders, even if the values of the object or array remain the same, a new reference is created.
- `React.memo` compares the references of props, not their contents, so it considers the prop to have changed and triggers a re-render
- To prevent unnecessary re-renders, you should memoize the objects or arrays using `useMemo` in the parent component. This ensures their references stay the same unless their values change.

```js
import React, { useMemo } from "react";

const Child = React.memo(({ data }) => {
  console.log("Child rendered");
  return <p>{data.value}</p>;
});

function Parent() {
  const [count, setCount] = React.useState(0);

  // Memoizing the object to retain its reference
  const data = useMemo(() => ({ value: "Hello, World!" }), []);

  console.log("Parent rendered");

  return (
    <div>
      <Child data={data} />
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default Parent;
```
## What are Pure Components?
- A Pure Component in React is a component that only re-renders if its props or state change.
- It uses shallow comparison `(===)` to determine if an update is needed.
- Helps optimize performance by preventing unnecessary re-renders.

```js
import React from "react";

const MyComponent = React.memo(({ name }) => {
  console.log("Re-rendered!");
  return <div>{name}</div>;
});
```

- Pure Components only perform a shallow comparison, meaning:
  - If primitive values `(string, number, boolean)` are the same, no re-render.
  - If objects or arrays change reference, even if content is the same, it re-renders.
```js
//Solution
const user = useMemo(() => ({ name: "John" }), []);
<MyComponent user={user} />;
```

## Does `React.lazy()` Support Named Exports?
- No, `React.lazy()` does NOT support named exports. It only works with default exports.
- `React.lazy()` expects a module that returns a default export.
- Named exports require destructuring, which `React.lazy()` does not support.

## What is Suspense Component?
- A built-in React component for handling lazy loading.
- Displays a fallback UI while waiting for the component to load.
- Works with `React.lazy()` and async data fetching (React 18+ with Suspense for Data Fetching).