---
type: lesson
status: draft
updated: 2026-04-11
tags:
  - react
  - fundamentals
---

# React - Lesson 01 - Foundations - Hooks, Composition, State, and Performance Basics

## Why it matters
This is the base layer for the rest of React. If the mental model is wrong here, everything later feels like magic or rules without reasons.

## Explanation
### Hooks
Hooks let function components participate in React state and side effects. They are positional, so call order must stay stable.

The practical lesson is simple: hooks are not mini lifecycle methods. They are how a component synchronizes with state, refs, context, layout, and external systems.

Each render gets its own closure snapshot, so hooks read the values from that render, not from some global "current" instance. That is why `useEffect` dependency arrays are correctness constraints rather than performance hints.

`useLayoutEffect` exists for the cases where you must read layout and update before paint. Most components should still prefer `useEffect`.

### Composition
React works best when components are composed, not inherited. `children` is often the cleanest extension point because it lets the consumer decide structure.

That is also why prop explosion is usually a design smell. If a component author is trying to anticipate every variation with configuration props, the API tends to become brittle. Compound components and render slots push structure back to the consumer while keeping behavior centralized.

### State ownership
Keep state as close as possible to where it is used. Lift it only when more than one child needs the same source of truth.

Context is useful when you need to share a value down the tree, but it is not a magic optimization. If the value changes often, every consumer is part of the update path.

### Performance basics
Most performance work starts with eliminating unnecessary re-renders structurally before reaching for memoization.

The best optimization is often to move state lower so an expensive sibling is never forced to re-render in the first place. Memoization is a second-line tool, not the foundation.

## Examples
```tsx
function Layout({ children }) {
  return <section>{children}</section>;
}

function App() {
  return (
    <Layout>
      <ExpensiveChart />
    </Layout>
  );
}
```

This keeps `ExpensiveChart` out of the parent re-render path as long as the parent is not recreating it locally.

```tsx
function SearchBox() {
  const [value, setValue] = useState('');
  return <input value={value} onChange={(e) => setValue(e.target.value)} />;
}
```

The state belongs with the field that owns it, not in a distant parent by default.

## Common misconceptions
- "Hooks are just lifecycle methods in a new syntax."
- "Dependencies are optional if the effect seems to work."
- "Lift state first, optimize later."
- "Memoization is the default performance solution."
- "A component only re-renders when the JSX it directly uses changes."

## Recap
The foundation is ownership and composition. Use hooks to manage local reactivity, use `children` and compound structure to shape APIs, and keep state near the UI that actually needs it.

## Link to exercises
- [[../../Exercises/React/React - Exercise 01 - Trace a Stale Closure]]
- [[../../Exercises/React/React - Exercise 04 - Refactor Prop Explosion]]

## Related concepts
- [[../../Concepts/React/React - Component Model, Props, and State]]
- [[../../Concepts/React/React - Hooks, Effects, and Closures]]
- [[../../Concepts/React/React - Composition, Lifting State, and Controlled vs Uncontrolled]]
- [[../../Concepts/React/React - Memoization and Performance Tradeoffs]]

## Sources
- User-provided React conversation transcript from 2026-04-11.
