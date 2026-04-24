---
type: lesson
status: draft
updated: 2026-04-11
tags:
  - react
  - performance
---

# React - Lesson 05 - Performance Beyond Memo

## Why it matters
Memoization is useful, but it is fragile and easy to overuse. Most real performance gains come from architecture first, memoization second, and imperative escape hatches only when necessary.

## Explanation
### Structural fixes first
Move state closer to where it matters. Extract expensive subtrees out of frequently updating parents. Avoid creating the re-render problem in the first place.

This is the cheapest win because it avoids work instead of trying to cache it.

### Memoization is conditional
`React.memo` works only when props are referentially stable. Inline objects, arrays, and callbacks break that stability unless you deliberately preserve it.

React compares props with shallow equality using `Object.is`. One fresh object literal is enough to invalidate the whole memo boundary.

### External stores need care
When state lives outside React, concurrent rendering can observe inconsistent snapshots unless the subscription model is designed for it.

`useSyncExternalStore` is the supported bridge for that case. It lets React subscribe to the store and verify snapshots so external state does not tear across a concurrent render.

### The compiler changes the direction of travel
The React compiler can automate a lot of memoization work, but only when components stay pure and predictable. That is why structural fixes and pure render logic matter more than manual memoization everywhere.

The practical implication is that you should prefer simple, pure components over hand-rolled caches that only exist to protect a memo boundary.

### Hot paths may bypass React
For very high-frequency interactions, refs and direct DOM updates can be a better fit than pushing every frame through React state.

That does not mean "avoid React"; it means use React for declarative state, and use imperative updates where the render loop itself would be the bottleneck.

## Examples
```tsx
const MemoizedChild = React.memo(function MemoizedChild({ style }) {
  return <p style={style}>Hello</p>;
});

function App() {
  const style = { color: 'red' };
  return <MemoizedChild style={style} />;
}
```

This memo boundary is weak because `App` creates a fresh `style` object on every render.

```tsx
function Draggable() {
  const ref = useRef<HTMLDivElement>(null);
  // pointer movement can update the DOM directly here
  return <div ref={ref} />;
}
```

For a hot path, this can be more appropriate than rerendering a deep tree on every move event.

## Common misconceptions
- "Memoization is the default optimization."
- "If a component is memoized once, it will stay fast."
- "A stable-looking object literal is stable enough."
- "React state is always the right place for every live value."
- "The compiler will optimize impure render logic for me."

## Recap
Performance work in React starts with tree shape and state ownership. Memoization is the pruning layer, not the foundation.

## Link to exercises
- [[../../Exercises/React/React - Exercise 05 - Memoization and External Store Reasoning]]

## Related concepts
- [[../../Concepts/React/React - Memoization and Performance Tradeoffs]]

## Sources
- User-provided React conversation transcript from 2026-04-11.
