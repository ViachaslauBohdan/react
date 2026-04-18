# ref as a normal prop

## Problem

Function components that needed a DOM ref historically used **`forwardRef`**, which added boilerplate and awkward typing. Passing `ref` through multiple layers was noisy.

## How to use

In React 19, **function components can accept `ref` as a regular prop** (where supported by your tooling). You forward it to a DOM element or another component as needed.

You can still use `forwardRef` for older patterns or libraries; migration is gradual.

## Examples

```jsx
import { useRef } from "react";

function Input({ label, ref }) {
  return (
    <label>
      {label}
      <input ref={ref} />
    </label>
  );
}

function Form() {
  const inputRef = useRef(null);
  return (
    <>
      <Input label="Name" ref={inputRef} />
      <button type="button" onClick={() => inputRef.current?.focus()}>
        Focus
      </button>
    </>
  );
}
```

```jsx
// Before (still valid): forwardRef((props, ref) => ...)
// After (React 19 style in many cases): function MyInput({ ref, ...props }) { ... }
```

> TypeScript: you may need updated `@types/react` so `ref` is recognized on your props type.
