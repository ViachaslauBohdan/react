# React DevTools overview

## Problem

React builds a **virtual tree** that can be hard to map to what you see on screen. Console logging `props` everywhere does not scale, and performance issues are invisible until you measure **what re-rendered** and **how expensive** each update was.

## What React DevTools is

**React DevTools** is a browser extension (Chrome, Firefox, Edge; also standalone in some setups) that adds two main panels to your dev tools:

1. **Components** — browse the React tree, inspect **props**, **state**, **hooks**, and **context** for the selected fiber.
2. **Profiler** — record an interaction and see **which components committed**, timing, and why updates happened (when the feature is available in your version).

It works with **function and class components** and is the standard way to debug React UIs during development.

## How to use (basics)

1. Install **“React Developer Tools”** from your browser’s extension store (publisher: Meta / React team).
2. Open your app in **development mode** (production builds strip helpful details).
3. Open the browser **Developer Tools** → find the **“⚛️ Components”** and **“⚛️ Profiler”** tabs.
4. Use the **Components** tab to click a node in the tree (or use “select element” / pick on page if your version supports it) and read **Props**, **State**, **Hooks**, etc., in the right-hand pane.

**Tips**

- Pin the tabs you use often; names vary slightly by browser.
- If the ⚛️ tabs are missing, the page might not be using React, or the extension may need permission for `file://` URLs (check extension settings).

## Examples (what you do in the UI)

1. Load your app → **Components** tab → click `<App>` → expand children until you find the component you care about.
2. Change a route or state in the app → watch the **highlighted** component in the tree update (if “highlight updates” is enabled in settings).
3. Switch to **Profiler** → click **Record** → perform a slow action → **Stop** → click a commit bar to see which components rendered in that frame.

For deeper workflows, see [component-tree-and-inspector.md](./component-tree-and-inspector.md) and [profiler-and-performance.md](./profiler-and-performance.md).
