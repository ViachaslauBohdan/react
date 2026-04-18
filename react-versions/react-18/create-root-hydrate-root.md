# createRoot / hydrateRoot

## Problem

`ReactDOM.render` and `ReactDOM.hydrate` mixed concerns and made it harder to add **concurrent features** and a clear **lifecycle for the root**. React 18 introduces explicit root objects.

## How to use

- **Client-only:** `createRoot(container).render(<App />)`
- **SSR:** `hydrateRoot(container, <App />)`

Import from `react-dom/client`. Remove legacy `ReactDOM.render` / `hydrate` when you upgrade.

## Examples

```jsx
import { createRoot } from "react-dom/client";
import App from "./App";

const container = document.getElementById("root");
const root = createRoot(container);
root.render(<App />);
```

```jsx
import { hydrateRoot } from "react-dom/client";
import App from "./App";

const container = document.getElementById("root");
hydrateRoot(container, <App />);
```
