# Fragments

## Problem

Components must often **return multiple sibling elements**. Before fragments, you wrapped them in an extra `<div>` (or similar), which broke layout (CSS grid/flex), semantics, or styling.

## How to use

Return a **fragment** to group children **without a wrapper node**:

- Short syntax: `<> ... </>` (no keys)
- Long syntax: `<React.Fragment key={...}> ... </React.Fragment>` when you need a **key** (e.g. in a list)

## Examples

```jsx
function Columns() {
  return (
    <>
      <td>Hello</td>
      <td>World</td>
    </>
  );
}
```

```jsx
function List({ items }) {
  return items.map((item) => (
    <React.Fragment key={item.id}>
      <dt>{item.term}</dt>
      <dd>{item.description}</dd>
    </React.Fragment>
  ));
}
```
