## Event Pooling
- React reused event objects to improve performance.
- Event properties were cleared after the event handler executed.
- Accessing event properties asynchronously (`setTimeout`, `Promise`, etc.) caused issues.
- To prevent this, `event.persist()` was used.

 After React 17 (No Event Pooling)

- React creates a new event object for each event (no reuse).
- Event properties are always available, even in async functions.
- No need to call `event.persist()` anymore.
- React became simpler and easier to debug.

```js
function EventPoolingExample() {
  const handleClick = (event) => {
    console.log(event.type); // ✅ Works

    setTimeout(() => {
      console.log(event.type); // ❌ Null (event is cleared)
    }, 1000);
  };

  return <button onClick={handleClick}>Click Me</button>;
}
```
- Fix: Use `event.persist()`
```js
function FixEventPooling() {
  const handleClick = (event) => {
    event.persist(); // Prevents clearing
    setTimeout(() => {
      console.log(event.type); // Works fine
    }, 1000);
  };

  return <button onClick={handleClick}>Click Me</button>;
}
```

## what does build folder contains?
After running `npm run build`, React generates a `build/` folder containing optimized production files.
1. `index.html` → Main HTML file (links to bundled JS & CSS).
2. `static/ Folder` → Stores optimized assets.
   - `js/` → Minified JavaScript files (React code).
   - `css/` → Minified CSS files.
   - `media/` → Images, fonts, etc.
3. `asset-manifest.json` → Maps assets for caching/CDN.
4. `robots.txt` → SEO file for search engine indexing.



## What is render hijacking in react?



## What is a HOC?

- A Higher-Order Component (HOC) is a function that takes a component as input and returns a new component with added functionality.
- It is used to reuse logic across multiple components.
- Always forward props using {...props}.
- Name HOCs with a prefix like `withSomething` (e.g., withAuth).
- Avoid overusing HOCs—they can lead to nested components.
- We can replace HOCs with Hooks which provide a more concise and readable way to reuse logic.


## How HOCs Work?

- Input: Takes a component (e.g., ComponentA).
- Enhancement: Adds extra logic or functionality.
- Output: Returns a new component with the original behavior plus the added functionality.

```
const withExtraProps = (WrappedComponent) => {
  return (props) => <WrappedComponent {...props} additionalProp="Extra Value" />;
};
```

```
const withAuth = (WrappedComponent) => {
  return (props) => {
    const isLoggedIn = true; // Logic
    return isLoggedIn ? <WrappedComponent {...props} /> : <div>Please log in</div>;
  };
};

const Dashboard = () => <h1>Dashboard</h1>;
const ProtectedDashboard = withAuth(Dashboard);

// Usage
<ProtectedDashboard />;
```

## Why Use HOCs?

- Reusability: Share logic without duplicating code.
- Abstraction: Keep components clean by abstracting additional functionality.
- Props Injection: Easily inject extra props into components.

## Common Use Cases of HOCs?

- Authentication: Restrict access to certain components.
- Logging: Track user interactions or log props.
- Analytics: Add tracking functionality.


