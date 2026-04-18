# Component tree and inspector

## Problem

You need to answer: **which component instance** produced this UI, **what props** did it receive, and **what state/hooks** does it hold right now? Guessing from source files is slow when composition and HOCs are involved.

## How to use

In the **Components** tab:

- **Tree view** — parent/child structure mirrors React’s fiber tree (with sensible collapsing). Click a node to select it.
- **Inspector pane** (usually on the right) shows, for the selected component:
  - **props** — current prop values (editable in dev for quick experiments in many versions).
  - **state** — class `state` or equivalent.
  - **hooks** — ordered list for function components (`useState`, `useMemo`, etc., depending on React/DevTools version).
  - **context** — which context values apply (when exposed).
- **Search** — filter the tree by name to jump faster in large apps.
- **“Highlight updates”** (in DevTools settings) — flashes components when they re-render; great for spotting unnecessary renders.

**Limitations (mental model)**

- You see **development** details; production may hide names or behave differently.
- Some third-party code may use **minified** display names unless the library sets `displayName`.

## Examples (workflow)

**Find why a list item looks wrong**

1. Open **Components**.
2. Use search or drill to `<ListItem>` (or your component name).
3. Read **props** — e.g. wrong `id` or `label` passed from parent.
4. Walk **up** the tree to the parent that owns the data.

**Spot a runaway re-render**

1. Enable **Highlight updates** in React DevTools settings.
2. Interact with the UI — components that flash on every keystroke or timer tick are re-rendering; pair this with the [Profiler](./profiler-and-performance.md) to quantify cost.

```text
Components tab
  └─ App
       └─ Layout
            └─ SearchInput    ← select: inspect props.value, callbacks
            └─ ResultsList
                 └─ Row (×N) ← compare props between rows
```
