## How to focus an input element on page load?
```js
import React, { useEffect, useRef } from "react";

const App = () => {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus(); // Focuses input when component mounts
  }, []);

  return <input ref={inputRef} type="text" placeholder="Type here..." />;
};

export default App;
```

##  How to import and export components using React and ES6?
### 1. Default Export
- A file can have only one default export.
- Import without curly braces, and the name can be any.
```js
// Exporting File: MyComponent.js
export default function MyComponent() {
    return <h1>Hello, I am the default export!</h1>;
}
```
```js
// Importing File: App.js 
import MyComponent from './MyComponent';

function App() {
    return (
        <div>
            <MyComponent />
        </div>
    );
}

export default App;
```
### 2. Named Export
- A file can have multiple named exports.
- Import using curly braces `{}` with exact names.
```js
// Exporting File: MyComponents.js
export function Header() {
    return <h1>This is the Header</h1>;
}

export function Footer() {
    return <h3>This is the Footer</h3>;
}

```
```js
// Importing File: App.js
import { Header, Footer } from './MyComponents';

function App() {
    return (
        <div>
            <Header />
            <Footer />
        </div>
    );
}

export default App;
```
### 3. Mixed Export
Use both default and named exports in the same file.
```js
// Exporting File: MyComponents.js
export default function Main() {
    return <p>This is the Main Component</p>;
}

export function Header() {
    return <h1>This is the Header</h1>;
}

export function Footer() {
    return <h3>This is the Footer</h3>;
}
```
```js
// Importing: File: App.js
import Main, { Header, Footer } from './MyComponents';

function App() {
    return (
        <div>
            <Header />
            <Main />
            <Footer />
        </div>
    );
}

export default App;
```

## How to use innerHTML in React?
```js
const content = "<p style='color: red;'>This is raw HTML</p>";

const MyComponent = () => (
  <div dangerouslySetInnerHTML={{ __html: content }} />
);
```
- It bypasses React’s default protection against XSS (Cross-Site Scripting).
- Only use it with trusted content to avoid security risks.

## How to pass numbers to React component?
```js
<MyComponent numberProp={42} />
```

```js
const myNumber = 100;
<MyComponent numberProp={myNumber} />
```

```js
//Passing a Number as a String (Not Recommended)
<MyComponent numberProp="42" />
```

## What are default props?
- Default props in React allow you to set default values for props when a parent component does not provide them.
```js
const Greeting = ({ name = "Guest" }) => {
  return <h2>Hello, {name}!</h2>;
};

export default Greeting;
```