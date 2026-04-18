# Automatic batching

## Problem

React has always batched **some** state updates inside React event handlers. Updates inside **timeouts**, **promises**, or **native events** often caused **extra renders**—one per `setState`—hurting performance.

## How to use

React 18 **automatically batches** multiple state updates from **anywhere** in most cases (including async code), so you get fewer intermediate renders without manual batching APIs.

If you ever need to **force** synchronous flushing (rare), React provides `flushSync` from `react-dom`—use sparingly.

## Examples

```jsx
import { useState } from "react";

function Demo() {
  const [a, setA] = useState(0);
  const [b, setB] = useState(0);

  function handleClick() {
    setTimeout(() => {
      setA((x) => x + 1);
      setB((y) => y + 1);
      // React 18: typically one re-render after both updates
    }, 0);
  }

  return (
    <button type="button" onClick={handleClick}>
      a={a} b={b}
    </button>
  );
}
```
