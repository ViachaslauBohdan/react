# use

## Problem

You sometimes need to **read a Promise or Context** during render in a way that **integrates with Suspense** (and error boundaries), instead of manually tracking loading flags everywhere.

## How to use

`use(resource)` is a React 19 API (import from `react`). It works with:

- A **Context** value.
- A **Promise** (in supported patterns)—when used with Suspense, the UI can wait on the promise via the nearest `<Suspense>` boundary.

**Rules:** Follow React’s rules of hooks—`use` must be called during render (not inside arbitrary callbacks in the same way as `useState`).

## Examples

```jsx
import { use, Suspense, createContext } from "react";

const ThemeContext = createContext("light");

function ThemedButton() {
  const theme = use(ThemeContext);
  return <button data-theme={theme}>OK</button>;
}
```

```jsx
// Promise + Suspense (pattern depends on how you create/cache the promise)
function Read({ promise }) {
  const value = use(promise);
  return <p>{value}</p>;
}

function App({ promise }) {
  return (
    <Suspense fallback={<p>Loading…</p>}>
      <Read promise={promise} />
    </Suspense>
  );
}
```

> In real apps, data frameworks often wrap promise creation and caching; the **idea** is: suspend at the boundary, not manual `useEffect` loading spaghetti.
