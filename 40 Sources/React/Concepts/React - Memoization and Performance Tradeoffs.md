---
type: concept
status: evergreen
updated: 2026-04-11
tags:
  - react
  - performance
  - memoization
  - frontend
---

# React - Memoization and Performance Tradeoffs

## Summary
Memoization is a pruning tool, not the default solution. It only helps when referential stability is preserved and when the skipped work is more expensive than the memo boundary.

## Core idea
The best performance fix is usually structural: move state lower, move expensive subtrees out of the re-render path, or keep hot paths outside React. Memoization is the second line of defense.

`React.memo` only helps when the incoming props stay referentially stable. One fresh object or callback is enough to break the boundary.

## Key rules
- `React.memo` compares props shallowly.
- Inline objects, arrays, and callbacks break referential equality.
- `useMemo` and `useCallback` help only when their dependencies are stable and the cached value matters.
- `useSyncExternalStore` is the correct way to read external mutable stores safely in concurrent rendering.
- The React compiler can automate memoization, but only for pure components it can reason about.
- For very hot paths, refs and direct DOM updates can be more appropriate than React state.

## Common mistakes
- Adding memoization everywhere by default.
- Using `useMemo` just to satisfy `React.memo`.
- Ignoring the cost of memoization itself.
- Forgetting that external stores can tear without the right subscription model.
- Assuming manual memoization is the final performance architecture.

## Related notes
- [[../../Lessons/React/React - Lesson 05 - Performance Beyond Memo]]
- [[../../Lessons/React/React - Lesson 06 - Concurrent React, Suspense, and Transitions]]
- [[../../Exercises/React/React - Exercise 05 - Memoization and External Store Reasoning]]

## Sources
- User-provided React conversation transcript from 2026-04-11.
- React docs: [memo](https://react.dev/reference/react/memo)
- React docs: [useMemo](https://react.dev/reference/react/useMemo)
- React docs: [useCallback](https://react.dev/reference/react/useCallback)
- React docs: [useSyncExternalStore](https://react.dev/reference/react/useSyncExternalStore)
- React compiler overview: [React Compiler](https://react.dev/learn/react-compiler)
