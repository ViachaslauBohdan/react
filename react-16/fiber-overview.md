# Fiber (overview)

## Problem

The classic React reconciler (often called “Stack”) struggled to **interrupt** long updates. Large trees could make the UI feel janky: one big render blocked everything behind it.

## How to use

**Fiber** is React 16’s reconciler architecture. As an app author you do not import “Fiber.” You benefit from:

- **Work can be split and prioritized** (foundation for later concurrent features in React 18+).
- Features like **error boundaries**, **portals**, and **fragments** build on this model.

Think of Fiber as **how** React schedules and applies updates—not a public API.

## Examples

There is no Fiber API snippet. Instead, you use normal React APIs; Fiber is the engine underneath.

```jsx
// You write this…
function App() {
  const [count, setCount] = React.useState(0);
  return <button onClick={() => setCount((c) => c + 1)}>{count}</button>;
}

// …React 16+ schedules updates using Fiber internally.
```

For user-visible concurrency (transitions, concurrent rendering), see **React 18** docs in this repo: `create-root-hydrate-root.md`, `start-transition-use-transition.md`.
