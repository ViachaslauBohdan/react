# React Compiler

## Problem

Fast React code often needs **manual memoization** (`useMemo`, `useCallback`, `memo`) to avoid wasted work. That is easy to get wrong, and it clutters components.

## How to use

The **React Compiler** is a **build-time** tool (Babel plugin) that analyzes your code and **inserts optimizations automatically** where safe—similar in spirit to how other languages optimize, but for React’s rules.

You **do not** import “Compiler” in application code. You enable it in your build pipeline and keep writing normal components.

**Status:** Rollout depends on version and ecosystem; follow official React docs for your setup.

## Examples

**Before (manual):**

```jsx
import { useMemo } from "react";

function List({ items, query }) {
  const filtered = useMemo(
    () => items.filter((x) => x.includes(query)),
    [items, query]
  );
  return (
    <ul>
      {filtered.map((x) => (
        <li key={x}>{x}</li>
      ))}
    </ul>
  );
}
```

**After (conceptual):** same readable code, compiler proves immutability / safety and memoizes where valid—**you still write idiomatic React**.

```jsx
function List({ items, query }) {
  const filtered = items.filter((x) => x.includes(query));
  return (
    <ul>
      {filtered.map((x) => (
        <li key={x}>{x}</li>
      ))}
    </ul>
  );
}
```

> The compiler only optimizes what it can **prove** is safe; you may still need explicit memoization for unusual cases.
