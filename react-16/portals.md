# Portals

## Problem

Some UI needs to **break out of the parent’s DOM hierarchy**—modals, dropdowns, full-screen overlays—often for z-index, `overflow`, or accessibility reasons. Nesting in place makes styling and stacking context painful.

## How to use

Call `ReactDOM.createPortal(child, domNode)` to render `child` into **any existing DOM node** (for example `document.body`), while keeping React context and event bubbling behavior as documented for your React version.

## Examples

```jsx
import { createPortal } from "react-dom";

function Modal({ open, children }) {
  if (!open) return null;
  return createPortal(
    <div role="dialog" className="modal">
      {children}
    </div>,
    document.body
  );
}
```

```jsx
function App() {
  const [open, setOpen] = React.useState(false);
  return (
    <>
      <button type="button" onClick={() => setOpen(true)}>
        Open
      </button>
      <Modal open={open}>
        <p>Hello from a portal.</p>
        <button type="button" onClick={() => setOpen(false)}>
          Close
        </button>
      </Modal>
    </>
  );
}
```
