# useSyncExternalStore

## Problem

Third-party **external stores** (not React state) need a safe subscription API that works with **concurrent rendering** and avoids **tearing** (reading different values in the same render pass).

## How to use

`useSyncExternalStore(subscribe, getSnapshot)` returns `getSnapshot()`’s value and re-renders when `subscribe` fires.

Library authors wrap stores; app code often uses a thin hook.

## Examples

```jsx
import { useSyncExternalStore } from "react";

const store = {
  getState: () => store.value,
  value: 0,
  listeners: new Set(),
  subscribe(fn) {
    store.listeners.add(fn);
    return () => store.listeners.delete(fn);
  },
  setValue(v) {
    store.value = v;
    store.listeners.forEach((fn) => fn());
  },
};

function useStore() {
  return useSyncExternalStore(
    store.subscribe,
    store.getState,
    store.getState // optional getServerSnapshot for SSR
  );
}

function Counter() {
  const n = useStore();
  return (
    <button type="button" onClick={() => store.setValue(n + 1)}>
      {n}
    </button>
  );
}
```

> In real apps, prefer established bindings (e.g. Redux Toolkit) that already use this pattern correctly.
