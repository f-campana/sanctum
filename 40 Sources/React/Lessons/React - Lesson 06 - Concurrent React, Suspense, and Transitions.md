---
type: lesson
status: draft
updated: 2026-04-11
tags:
  - react
  - concurrency
  - suspense
---

# React - Lesson 06 - Concurrent React, Suspense, and Transitions

## Why it matters
Concurrent React changes user experience. It lets React keep the current UI visible while preparing lower-priority work in the background.

## Explanation
### Transitions
`startTransition` marks work as non-urgent. That lets urgent updates like typing, selection, or button feedback stay responsive.

The point is not "make everything slow updates faster." The point is to let React prioritize the thing the user is actively doing over the thing that can wait.

React also tracks update priority internally, so urgent input beats lower-priority work. You do not control lanes directly, but they explain why a transition can wait while a click or keystroke goes first.

### Suspense
Suspense lets a component declare that it is waiting on async work. React can then show a fallback boundary while the data or code arrives.

If a child suspends, React can switch the nearest boundary to its fallback. If the update that caused the suspend was wrapped in a transition, React can often keep showing already-visible content instead of flashing the fallback immediately.

### Old UI can stay on screen
The key concurrency win is not faster data fetching. It is that React can keep showing the previous committed tree while it prepares the next one.

That is what makes the user experience feel stable: the old tree stays current while the new tree is built in a separate work-in-progress tree.

This behavior only exists because Fiber can maintain two trees at once.

### External stores and tearing
Concurrent rendering assumes React controls the state snapshot. External mutable stores need a correct subscription model to avoid inconsistent reads.

### Streaming and hydration
When server rendering is combined with Suspense, React can stream fallbacks first and hydrate or reveal deeper content later. The important idea is progressive disclosure, not all-or-nothing loading.

Streaming and selective hydration make the browser useful sooner instead of waiting for the whole tree to become interactive.

## Examples
```tsx
const [isPending, startTransition] = useTransition();

startTransition(() => {
  setTab('profile');
});
```

The tab change is treated as background work.

```tsx
<Suspense fallback={<Skeleton />}>
  <Profile />
</Suspense>
```

If `Profile` suspends, React can show the fallback boundary while it waits.

## Common misconceptions
- "Concurrent means multi-threaded."
- "Suspense is just a loading spinner API."
- "Transitions only matter for data fetching."
- "The old UI disappears as soon as the next render starts."

## Recap
Concurrency is a scheduling model. React can pause, resume, or abandon renders, but it still commits one coherent tree at a time.

## Link to exercises
- [[../../Exercises/React/React - Exercise 06 - Transition UX and Suspense]]

## Related concepts
- [[../../Concepts/React/React - Rendering and Re-rendering]]
- [[../../Concepts/React/React - Memoization and Performance Tradeoffs]]
- [[../../Concepts/React/React - Concurrent React, Suspense, and Transitions]]

## Sources
- User-provided React conversation transcript from 2026-04-11.
