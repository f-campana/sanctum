---
type: lesson
status: draft
updated: 2026-04-11
tags:
  - react
  - rendering
  - hooks
---

# React - Lesson 02 - Rendering, Closures, and Re-rendering

## Why it matters
This is where most React bugs become explainable: stale closures, surprising logs, and "why did this component re-render?" all come from the render snapshot model.

## Explanation
### Render is a snapshot
Every render is a new invocation of the component function. Any local variables, callbacks, or effects created there belong to that specific render.

That means render is pure computation: React calls your component to get a new description of UI. It has not touched the DOM yet. The DOM changes later, during commit.

### Closures freeze values
Event handlers and timers do not magically track future state. They capture the state that existed when the render created them.

This is why a delayed callback can log an older value even though the UI has since updated. The callback is still pointing at the old closure.

### Render and commit are different
Render computes the next UI. Commit applies the chosen result to the DOM. Side effects belong outside render.

React can re-run render work more than once, and in concurrent mode it can abandon a render that never reaches commit. That is why render must stay pure.

### Why re-renders happen
A component re-renders because its own state changed, its parent re-rendered, or its context changed. React does not magically know which child "needs" the update and skip the rest by default.

When a parent re-renders, React re-invokes its children too. React skips work only when a bailout condition applies, such as stable identity through `memo` or structurally isolating a subtree.

If you need a mutable value that survives renders without triggering more renders, `useRef` is the usual escape hatch.

## Examples
```tsx
function Counter() {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    setCount(count + 1);
    setTimeout(() => console.log(count), 3000);
  };

  return <button onClick={handleClick}>{count}</button>;
}
```

The timeout logs the value captured by the click's render, not the value three seconds later.

```tsx
function Parent() {
  const [count, setCount] = useState(0);
  return (
    <>
      <button onClick={() => setCount((c) => c + 1)}>{count}</button>
      <Child />
    </>
  );
}
```

`Child` re-renders because `Parent` re-renders, even if `Child` does not read `count`.

## Common misconceptions
- "If the DOM didn't change, the component didn't re-render."
- "React only calls components that directly use the changing state."
- "A closure sees the latest state automatically."
- "Effects are part of render."

## Recap
React is easier to reason about when you remember that each render is a snapshot. Closures point at that snapshot, and re-renders are the normal consequence of state ownership and parent updates.

## Link to exercises
- [[../../Exercises/React/React - Exercise 01 - Trace a Stale Closure]]
- [[../../Exercises/React/React - Exercise 02 - Predict Re-renders]]

## Related concepts
- [[../../Concepts/React/React - Hooks, Effects, and Closures]]
- [[../../Concepts/React/React - Rendering and Re-rendering]]

## Sources
- User-provided React conversation transcript from 2026-04-11.
