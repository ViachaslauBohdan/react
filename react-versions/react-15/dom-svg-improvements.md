# DOM and SVG improvements

## Problem

Earlier React versions had more **rough edges** around HTML attributes, SVG tags, and how updates hit the real DOM. That showed up as warnings, incorrect attributes, or subtle rendering bugs in SVG-heavy UIs.

## How to use

You rarely “turn on” this feature—it shipped with React 15. The win is knowing that **common DOM and SVG cases became more predictable**, so you spend less time fighting the reconciler for standard markup.

When upgrading old code, prefer **standard DOM property names** React expects (e.g. `className`, `htmlFor`) and valid SVG elements.

## Examples

```jsx
// SVG usage became more reliable across common cases in React 15+
function Icon() {
  return (
    <svg viewBox="0 0 24 24" width="24" height="24" aria-hidden="true">
      <circle cx="12" cy="12" r="10" />
    </svg>
  );
}
```

```jsx
// Unknown DOM attributes are passed through more predictably in modern React;
// prefer documented props for clarity.
function Box(props) {
  return <div data-testid="box" {...props} />;
}
```
