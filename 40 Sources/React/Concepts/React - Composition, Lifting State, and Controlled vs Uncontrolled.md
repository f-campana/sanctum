---
type: concept
status: evergreen
updated: 2026-04-11
tags:
  - react
  - composition
  - state
  - frontend
---

# React - Composition, Lifting State, and Controlled vs Uncontrolled

## Summary
Composition lets consumers decide structure while the component author keeps control over behavior. Lifting state and choosing controlled vs uncontrolled APIs are the main tools for managing shared ownership.

## Core idea
Good React architecture usually moves from "configuration props everywhere" toward "small composable pieces with clear ownership." Put state where it is needed, not where it might someday be convenient.

Passing JSX as `children` is often the cleanest way to let the consumer decide layout while the component author owns behavior.

## Key rules
- Use `children` to let consumers supply structure.
- Use compound components when one behavior needs several coordinated surfaces.
- Lift state to the nearest common owner when siblings need the same truth.
- Use controlled components when the parent must own the value.
- Use uncontrolled components when internal state is sufficient and the parent only needs notifications.

## Common mistakes
- Prop explosion.
- Over-lifting state.
- Mixing controlled and uncontrolled behavior in the same API.
- Exposing implementation details instead of a stable compositional surface.

## Related notes
- [[../../Lessons/React/React - Lesson 01 - Foundations - Hooks, Composition, State, and Performance Basics]]
- [[../../Lessons/React/React - Lesson 04 - Advanced Patterns at Scale]]
- [[../../Exercises/React/React - Exercise 04 - Refactor Prop Explosion]]

## Sources
- User-provided React conversation transcript from 2026-04-11.
- React docs: [Passing JSX as children](https://react.dev/learn/passing-props-to-a-component#passing-jsx-as-children)
- React docs: [Sharing state between components](https://react.dev/learn/sharing-state-between-components)
