# useId

## Problem

SSR and hydration need **stable IDs** for accessibility (`id`/`htmlFor`, `aria-*`) and labels. Random IDs per render break hydration; hand-written IDs collide across instances.

## How to use

Call `useId()` in a component to get a **stable, unique ID string** that matches on server and client. Use it for attributes, not as a list **key** for dynamic collections (use your data’s id for that).

## Examples

```jsx
import { useId } from "react";

function Field({ label }) {
  const id = useId();
  return (
    <>
      <label htmlFor={id}>{label}</label>
      <input id={id} />
    </>
  );
}
```

```jsx
function TwoFields() {
  return (
    <>
      <Field label="Name" />
      <Field label="Email" />
    </>
  );
}
// Each Field gets its own stable id pair.
```
