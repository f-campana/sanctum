---
type: concept
status: evergreen
updated: 2026-04-11
tags:
  - react
  - frontend
---

# React - Component Model, Props, and State

## Summary
React components are functions of props and state that return UI descriptions. Props flow in, state lives with the component that owns it, and identity is preserved by type, position, and key.

## Core idea
The component model is not "objects with methods." It is "pure render function plus reactive state." The component decides what to show from its current inputs, then React compares the result against the previous render.

Identity is preserved by type, position, and key, so the same visual slot is not automatically the same logical instance unless React can match it that way.

## Key rules
- Props are inputs from the parent.
- State is local, mutable through React, and should live as close as possible to where it is used.
- A component re-renders when its own state changes, when its parent re-renders, or when consumed context changes.
- Lifting state up is the fix when siblings need the same source of truth.
- Controlled components get their value from props; uncontrolled components keep the value internally and expose it through refs or callbacks.
- Composition usually beats prop explosion.

## Common mistakes
- Treating props as mutable state.
- Lifting state too high "just in case."
- Mixing ownership: one component both stores and derives the same value.
- Using global state before the local boundary is actually too small.
- Building an API with too many ad hoc configuration props instead of composable slots.

## Related notes
- [[../../Lessons/React/React - Lesson 01 - Foundations - Hooks, Composition, State, and Performance Basics]]
- [[../../Lessons/React/React - Lesson 04 - Advanced Patterns at Scale]]
- [[../../Exercises/React/React - Exercise 04 - Refactor Prop Explosion]]

## Sources
- User-provided React conversation transcript from 2026-04-11.
- React docs: [Components](https://react.dev/reference/react/components)
