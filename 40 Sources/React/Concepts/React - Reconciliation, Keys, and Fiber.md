---
type: concept
status: evergreen
updated: 2026-04-11
tags:
  - react
  - fiber
  - reconciliation
  - frontend
---

# React - Reconciliation, Keys, and Fiber

## Summary
Reconciliation is the process of matching a new React tree against the previous one. Keys and element types determine identity, while Fiber is the bookkeeping structure that lets React interrupt and resume work.

## Core idea
React does not diff every possible tree shape. It uses stable heuristics: same type and key means same identity; different type usually means replacement.

Fiber is the data structure behind that heuristic. It keeps the current tree and a work-in-progress tree so React can pause and resume rendering without losing the committed UI.

## Key rules
- Same element type and key preserve identity.
- Different type at the same position usually destroys state.
- Keys are about identity, not just list rendering.
- Fiber stores work-in-progress state, parent/child/sibling links, and update metadata.
- React keeps a current tree and a work-in-progress tree, linked by `alternate`.
- Concurrent rendering is possible because React can work on a separate tree before commit.
- The work loop can pause and resume without recursion.

## Common mistakes
- Using index keys for dynamic lists.
- Expecting state to survive a type change.
- Treating keys as a list-only concept.
- Assuming reconciliation means a full DOM rebuild.
- Forgetting that state follows fiber identity, not visual position alone.

## Related notes
- [[../../Lessons/React/React - Lesson 03 - Reconciliation, Keys, and Fiber]]
- [[../../Lessons/React/React - Lesson 06 - Concurrent React, Suspense, and Transitions]]
- [[../../Exercises/React/React - Exercise 03 - Keys, Identity, and State Preservation]]

## Sources
- User-provided React conversation transcript from 2026-04-11.
- React docs: [Preserving and resetting state](https://react.dev/learn/preserving-and-resetting-state)
