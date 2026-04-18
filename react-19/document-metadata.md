# Document metadata

## Problem

`<title>` and `<meta>` often lived only in static HTML or framework-specific head APIs, **far from the component** that actually knows the page context (route, data, locale).

## How to use

React 19 lets you **render document metadata inside the tree** (e.g. `<title>`, `<meta>`, `<link>`) and hoists it appropriately in supported environments. Colocate metadata with the screen that owns it.

Exact behavior can depend on your **framework** (Next.js, etc.) and SSR setup.

## Examples

```jsx
function ArticlePage({ title, description }) {
  return (
    <>
      <title>{title}</title>
      <meta name="description" content={description} />
      <article>
        <h1>{title}</h1>
        <p>…</p>
      </article>
    </>
  );
}
```

```jsx
function Profile({ user }) {
  return (
    <>
      <title>{user.name} · Profile</title>
      <main>{/* … */}</main>
    </>
  );
}
```

> Verify support in your meta-framework; the **idea** is colocation and fewer duplicated head templates.
