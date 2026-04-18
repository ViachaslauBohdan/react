# useOptimistic

## Problem

After the user submits something, waiting on the network makes the UI feel sluggish. **Optimistic UI** shows the expected outcome immediately, then reconciles if the server disagrees.

## How to use

`useOptimistic(state, reducer)` gives you an **optimistic** value you can update instantly when starting an action, while the real `state` catches up when the async work finishes.

Pair with transitions or form actions depending on your app.

## Examples

```jsx
import { useOptimistic } from "react";

export function Chat({ messages, sendMessage }) {
  const [optimistic, addOptimistic] = useOptimistic(messages, (state, newMsg) => [
    ...state,
    { ...newMsg, sending: true },
  ]);

  async function onSend(text) {
    const id = crypto.randomUUID();
    addOptimistic({ id, text });
    await sendMessage({ id, text });
  }

  return (
    <ul>
      {optimistic.map((m) => (
        <li key={m.id}>
          {m.text} {m.sending ? "…" : ""}
        </li>
      ))}
    </ul>
  );
}
```
