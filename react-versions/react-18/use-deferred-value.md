# useDeferredValue

## Problem

You have a **value that updates often** (search text) and **derived UI** that is expensive to render (big list). Re-rendering everything on every keystroke can stutter.

## How to use

`useDeferredValue(value)` returns a **lagging** version of `value`. React can keep the deferred value behind briefly so fast updates (the live input) stay smooth while expensive children catch up.

Pairs well with `React.memo` on slow child components.

## Examples

```jsx
import { useState, useDeferredValue, memo } from "react";

const allItems = ["apple", "apricot", "banana", "cherry"];

const SlowList = memo(function SlowList({ query }) {
  const items = allItems.filter((x) => x.includes(query)); // pretend this is expensive
  return (
    <ul>
      {items.map((x) => (
        <li key={x}>{x}</li>
      ))}
    </ul>
  );
});

function App() {
  const [q, setQ] = useState("");
  const deferred = useDeferredValue(q);

  return (
    <>
      <input value={q} onChange={(e) => setQ(e.target.value)} />
      <SlowList query={deferred} />
    </>
  );
}
```
