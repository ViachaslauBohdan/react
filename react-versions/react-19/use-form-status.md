# useFormStatus

## Problem

Child components (submit buttons, spinners) need to know whether the **parent form’s** submission is still running. Passing `isPending` through every layer gets old fast.

## How to use

`useFormStatus()` reads status from the **closest parent `<form>`** (must be under a form that is using Actions / `action` in a supported way). It returns fields like **`pending`**.

**Note:** This hook is meant for **child** UI of the form, not the component that defines the action in every setup—check your framework docs for boundaries.

## Examples

```jsx
import { useFormStatus } from "react-dom";

function SubmitButton({ label }) {
  const { pending } = useFormStatus();
  return (
    <button type="submit" disabled={pending}>
      {pending ? "Working…" : label}
    </button>
  );
}

export function NewsletterForm({ action }) {
  return (
    <form action={action}>
      <input name="email" type="email" />
      <SubmitButton label="Subscribe" />
    </form>
  );
}
```

> `useFormStatus` lives in **`react-dom`**, not `react`.
