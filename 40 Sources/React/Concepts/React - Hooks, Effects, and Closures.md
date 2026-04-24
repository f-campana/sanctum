---
type: concept
status: evergreen
updated: 2026-04-11
tags:
  - react
  - hooks
  - frontend
---

# React - Hooks, Effects, and Closures

## Summary
Hooks let function components use state, effects, refs, memoization, and context. Each render creates a snapshot, so closures capture the values from that render.

## Core idea
Hooks are positional: React matches each hook call by order. Effects are for synchronization with external systems, not for "running after render" as a lifecycle reflex.

Each render creates a snapshot, so closures capture the values from that render. That is why stale callbacks happen and why dependency arrays are correctness contracts.

## Key rules
- Call hooks unconditionally and in the same order every render.
- Use `useState` for values that should trigger re-rendering.
- Use `useRef` for mutable values that should persist without re-rendering.
- Use `useEffect` for side effects and synchronization.
- Use `useLayoutEffect` only when you must read layout before paint.
- Treat dependency arrays as correctness contracts.
- Prefer the updater form when the next state depends on the previous one.
- Use custom hooks to package one synchronization concern into a reusable abstraction.

## Common mistakes
- Calling hooks conditionally.
- Using `useEffect` as a data derivation step.
- Ignoring stale closures in event handlers, timers, and async callbacks.
- Lying in dependency arrays to silence the linter.
- Using refs as a hidden store for values that should actually drive UI.
- Reaching for `useLayoutEffect` when `useEffect` is sufficient.

## Related notes
- [[../../Lessons/React/React - Lesson 01 - Foundations - Hooks, Composition, State, and Performance Basics]]
- [[../../Lessons/React/React - Lesson 02 - Rendering, Closures, and Re-rendering]]
- [[../../Exercises/React/React - Exercise 01 - Trace a Stale Closure]]
- [[../../Exercises/React/React - Exercise 02 - Predict Re-renders]]

## Sources
- User-provided React conversation transcript from 2026-04-11.
- React docs: [useEffect](https://react.dev/reference/react/useEffect)
- React docs: [useLayoutEffect](https://react.dev/reference/react/useLayoutEffect)
- React docs: [useState](https://react.dev/reference/react/useState)
- React docs: [useRef](https://react.dev/reference/react/useRef)
