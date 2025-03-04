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

