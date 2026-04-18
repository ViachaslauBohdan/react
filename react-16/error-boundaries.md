# Error boundaries

## Problem

Before error boundaries, a **single thrown error** during rendering could break the whole UI. You could not declaratively say “if this subtree fails, show a fallback.”

## How to use

Use a **class component** that implements `static getDerivedStateFromError` and/or `componentDidCatch` (React 16+). Wrap risky subtrees (lazy routes, third-party widgets) with this boundary.

Error boundaries **do not** catch errors in event handlers, async code, or SSR the same way—plan separate error handling there.

## Examples

```jsx
import React from "react";

class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError() {
    return { hasError: true };
  }

  componentDidCatch(error, info) {
    console.error(error, info.componentStack);
  }

  render() {
    if (this.state.hasError) {
      return <p>Something went wrong here.</p>;
    }
    return this.props.children;
  }
}

export default ErrorBoundary;
```

```jsx
<ErrorBoundary>
  <RiskyWidget />
</ErrorBoundary>
```
