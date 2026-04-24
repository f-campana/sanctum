---
type: concept
status: evergreen
updated: 2026-04-11
tags:
  - react
  - rendering
  - frontend
---

# React - Rendering and Re-rendering

## Summary
Rendering is React calling a component to produce a new UI description. Re-rendering does not mean the DOM changed; it means React recomputed what the UI should be.

## Core idea
React renders top-down. When a parent re-renders, its children are re-invoked unless React can bail out with identity checks or explicit memoization.

Render is pure computation; commit is where DOM changes happen. In concurrent mode, a render can be restarted or abandoned before commit.

## Key rules
- Render is pure computation.
- Commit is where React mutates the DOM.
- A render may be restarted or discarded in concurrent mode.
- A component re-renders because its own state changed, its parent re-rendered, or its context changed.
- A render can be cheap even when it happens often; the problem is usually expensive subtrees.

## Common mistakes
- Equating "re-render" with "DOM update."
- Assuming React only re-renders components that directly read the changed state.
- Using render work for side effects.
- Forgetting that fresh object and function literals break referential equality.

## Related notes
- [[../../Lessons/React/React - Lesson 02 - Rendering, Closures, and Re-rendering]]
- [[../../Lessons/React/React - Lesson 03 - Reconciliation, Keys, and Fiber]]
- [[../../Exercises/React/React - Exercise 02 - Predict Re-renders]]

## Sources
- User-provided React conversation transcript from 2026-04-11.
- React docs: [Rendering and Commit](https://react.dev/learn/render-and-commit)
