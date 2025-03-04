## Event Pooling
- React reuses event objects for performance optimization. After an event handler runs, its properties are cleared (set to null) to reduce memory usage.

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
- Event objects are reused to optimize performance.
- Accessing event properties asynchronously? Use `event.persist()`.
- Prevents unnecessary memory usage and garbage collection.