# PureComponent

## Problem

Class components extend `React.Component` and **re-render by default** whenever the parent re-renders—even when `props` and `state` did not meaningfully change. That wasted work in large lists or frequently updating parents.

## How to use

Subclass `React.PureComponent` instead of `Component`. React will do a **shallow compare** of `props` and `state` before re-rendering. If nothing shallow-changed, the update is skipped.

**Caveat:** If you pass new object/array/function instances every render from the parent, shallow equality fails and you still re-render. Prefer stable references or immutability patterns.

## Examples

```jsx
import React, { PureComponent } from "react";

class UserRow extends PureComponent {
  render() {
    const { id, name } = this.props;
    return (
      <tr>
        <td>{id}</td>
        <td>{name}</td>
      </tr>
    );
  }
}

// Parent should pass the same object identity when data didn't change,
// or update props immutably so PureComponent can detect changes.
```

```jsx
// Bad for PureComponent: new object every parent render
<UserRow user={{ id: 1, name: "Ada" }} />

// Better: lift the object up or memoize in the parent
const user = { id: 1, name: "Ada" };
<UserRow user={user} />
```
