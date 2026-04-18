# New JSX transform

## Problem

Classic JSX compiled to `React.createElement(...)`, so every file using JSX needed **`import React from "react"`** even when you did not reference `React` directly. That was noisy and easy to forget.

## How to use

With the **new JSX transform** (Babel / TypeScript / bundler support), the compiler imports the **automatic** `jsx`/`jsxs` helpers for you. You can omit the default React import in modules that only use JSX.

**Setup:** enable the new transform in your compiler (e.g. Babel preset-react `runtime: "automatic"`). React 17+ ships the runtime entry points.

## Examples

**Before (classic transform):**

```jsx
import React from "react";

export function Hello() {
  return <h1>Hi</h1>;
}
```

**After (new transform; no default React import required for JSX-only files):**

```jsx
export function Hello() {
  return <h1>Hi</h1>;
}
```

You still import hooks or APIs you use by name:

```jsx
import { useState } from "react";

export function Counter() {
  const [n, setN] = useState(0);
  return <button onClick={() => setN(n + 1)}>{n}</button>;
}
```
