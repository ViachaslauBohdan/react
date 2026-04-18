# Profiler and performance

## Problem

The UI **feels slow**, but you do not know **which subtree** is expensive or **how many times** components re-rendered during one user action. Guessing leads to premature `memo` everywhere.

## How to use

Open the **Profiler** tab:

1. Click **Record** (blue circle).
2. Perform the interaction you care about (open a modal, type in search, navigate).
3. Click **Stop**.
4. Inspect **commits** (bars along the timeline). Each commit corresponds to a React render pass applying to the DOM.
5. Click a commit → see **which components** rendered and **time spent** (flame chart / ranked view depending on version).

**What to look for**

- **Tall/wide bars** — expensive subtrees; optimize data flow or split work (`startTransition` in React 18+, etc.).
- **Many small renders** — possible unnecessary parent updates; check props identity and context subscribers.
- **“Why did this render?”** — when available, explains prop/state/context changes for a selected update (exact UI depends on DevTools + React version).

**Good habits**

- Profile **one scenario at a time** (e.g. “filter list with 10k rows”).
- Compare **before/after** when you add `memo`, context splits, or concurrent features.

## Examples (minimal checklist)

```text
Profiler
  Record → type in search box → Stop
    Commit #12  ~8ms
      SearchBox        0.1ms
      ResultsList      5.2ms   ← investigate children here
        Row (×200)     4.8ms
```

**Pair with code-level fixes** (see version docs in this repo):

- React 18: [start-transition-use-transition.md](../react-18/start-transition-use-transition.md), [use-deferred-value.md](../react-18/use-deferred-value.md).
- React 19: [react-compiler.md](../react-19/react-compiler.md) (optional automated memoization).
