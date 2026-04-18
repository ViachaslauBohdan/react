# useActionState

## Problem

Forms often need **pending state**, **error handling**, and **sequential updates** from async work (server actions, mutations). Wiring `useState` + `useTransition` by hand gets repetitive and easy to get wrong.

## How to use

`useActionState(action, initialState)` (React 19) returns `[state, dispatch, isPending]`. Your **action** receives `(previousState, formData)` when used with forms, or you can dispatch payloads depending on your pattern.

Works well with **`<form action={...}>`** and progressive enhancement when your stack supports it.

## Examples

```jsx
import { useActionState } from "react";

async function submitAction(prevState, formData) {
  const name = formData.get("name");
  await new Promise((r) => setTimeout(r, 300));
  return { ok: true, message: `Saved ${name}` };
}

export function Form() {
  const [state, formAction, isPending] = useActionState(submitAction, {
    ok: false,
    message: "",
  });

  return (
    <form action={formAction}>
      <input name="name" />
      <button type="submit" disabled={isPending}>
        {isPending ? "Saving…" : "Save"}
      </button>
      {state.message ? <p>{state.message}</p> : null}
    </form>
  );
}
```

> Exact signatures vary slightly by framework (e.g. Next.js server actions). The **mental model** is: one hook ties **async work** to **form-driven state**.
