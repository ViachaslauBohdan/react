# Suspense

## Problem

You need a **declarative loading state** while something asynchronous happens—lazy-loaded code, or async data patterns your app/framework supports—without scattering `if (loading)` everywhere.

## How to use

Wrap a subtree in `<Suspense fallback={...}>`. When a child **suspends** (throws a promise in supported data/lazy patterns), React shows `fallback` until the content is ready.

**`React.lazy`** is the simplest built-in case: dynamic `import()` for components.

## Examples

```jsx
import React, { Suspense, lazy } from "react";

const Profile = lazy(() => import("./Profile"));

function App() {
  return (
    <Suspense fallback={<p>Loading profile…</p>}>
      <Profile />
    </Suspense>
  );
}
```

```jsx
// While Profile.js loads, users see the fallback.
// After load, Profile renders normally.
```

> **Note:** Data fetching with Suspense depends on a compatible data layer (or framework). The **pattern** is the same: suspend → show fallback.
