# useInsertionEffect

## Problem

CSS-in-JS libraries inject **style tags** when components mount. If they inject during `useLayoutEffect`, they can be **too late** compared to layout reads. If they use `useEffect`, users can see a **flash of unstyled content**.

## How to use

`useInsertionEffect` runs **before** `useLayoutEffect`, **after** DOM mutations from React are known. Use it to inject global or scoped styles **before** paint-critical layout effects run.

**Do not** trigger state updates that user code depends on here—this hook targets **library-style injection**.

## Examples

```jsx
import { useInsertionEffect } from "react";

function useCss(rule) {
  useInsertionEffect(() => {
    const style = document.createElement("style");
    style.textContent = rule;
    document.head.append(style);
    return () => style.remove();
  }, [rule]);
}

function Box() {
  useCss(".box{color:blue}");
  return <div className="box">Hi</div>;
}
```

> Most application code never needs this hook directly—style libraries use it internally.
