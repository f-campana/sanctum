---
type: concept
status: evergreen
updated: 2026-04-11
tags:
  - react
  - concurrency
  - suspense
  - frontend
---

# React - Concurrent React, Suspense, and Transitions

## Summary
Concurrent React lets React prepare work in the background, pause and resume rendering, and keep the current UI visible while lower-priority updates are prepared. Suspense provides the boundary for waiting on async work, and transitions mark updates as non-urgent.

## Core idea
React is still single-threaded. "Concurrent" means cooperative scheduling, not parallel execution. React can keep one committed tree on screen while it builds a separate work-in-progress tree.

That is why transitions can keep already-visible content on screen while lower-priority work is prepared in the background.

## Key rules
- Use `startTransition` or `useTransition` for non-urgent UI updates.
- Use `isPending` to show a subtle pending state instead of a full loading flash.
- Use `Suspense` boundaries to define where fallback UI should appear.
- Treat transitions as interruptible work.
- Remember that React's own state is consistent within a render pass, but external stores can tear without the right subscription protocol.

## Common mistakes
- Thinking concurrent means multi-threaded.
- Using transitions to control text input values.
- Treating Suspense as a generic spinner helper instead of a boundary system.
- Showing fallback UI too early and hiding already-visible content unnecessarily.

## Related notes
- [[../../Lessons/React/React - Lesson 06 - Concurrent React, Suspense, and Transitions]]
- [[../../Exercises/React/React - Exercise 06 - Transition UX and Suspense]]
- [[../../Concepts/React/React - Memoization and Performance Tradeoffs]]
- [[../../Concepts/React/React - Rendering and Re-rendering]]

## Sources
- User-provided React conversation transcript from 2026-04-11.
- React blog: [React v18](https://react.dev/blog/2022/03/29/react-v18)
- React docs: [useTransition](https://react.dev/reference/react/useTransition)
- React docs: [Suspense](https://react.dev/reference/react/Suspense)
- React docs: [useSyncExternalStore](https://react.dev/reference/react/useSyncExternalStore)
