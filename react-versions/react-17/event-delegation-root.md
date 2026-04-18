# Event delegation at the root

## Problem

Older React attached listeners at the **document** level. That made **multiple React versions on one page** (gradual migration) harder: events could cross “version boundaries” in surprising ways.

## How to use

React 17 attaches the event listener to the **DOM node where you mounted React** (the “root”), not `document`. You do not change your JSX—`onClick`, `onChange`, etc. look the same.

**Why it matters:** safer **incremental upgrades** (micro-frontends, embedded widgets) and more predictable bubbling relative to the rest of the page.

## Examples

```jsx
import ReactDOM from "react-dom";
import App from "./App";

// React 17: mount once on your container; events delegate from this root (not document).
ReactDOM.render(<App />, document.getElementById("root"));
```

```jsx
// Your code stays idiomatic
function App() {
  return (
    <button type="button" onClick={() => console.log("clicked")}>
      OK
    </button>
  );
}
```

> **Note:** React 18 prefers `createRoot` from `react-dom/client` instead of `ReactDOM.render`—see [create-root-hydrate-root.md](../react-18/create-root-hydrate-root.md). Delegation still attaches to the mount container for that root.
