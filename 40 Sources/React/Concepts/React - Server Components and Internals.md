---
type: concept
status: evergreen
updated: 2026-04-11
tags:
  - react
  - server-components
  - internals
  - frontend
---

# React - Server Components and Internals

## Summary
Server Components keep data-heavy, non-interactive UI on the server so the client bundle stays smaller. React internals such as Fiber, the hooks list, the work loop, and the scheduler explain how render interruption, reconciliation, and state preservation work.

## Core idea
React's model extends beyond the browser. A Server Component tree is serialized and reconciled on the client, while the Fiber architecture and scheduler make the render pipeline interruptible and resumable.

Server Components are the default in modern RSC-enabled frameworks, and Client Components opt in with `'use client'` when they need state, effects, or browser APIs.

## Key rules
- Server Components can fetch data directly and do not ship their implementation to the client.
- Client Components opt in to browser interactivity with `'use client'`.
- A Server Component can render a Client Component, but not the other way around.
- React uses Fiber to keep a current tree and a work-in-progress tree.
- Hooks are stored as a linked list on the fiber and are read in call order.
- The scheduler and lanes let React prioritize urgent work over transitions.

## Common mistakes
- Treating Server Components as "just SSR."
- Importing Server-only logic into Client Components.
- Thinking Fiber is only for library authors.
- Assuming React always runs the whole tree synchronously from top to bottom.
- Assuming ordinary Server Components use a `use server` directive.

## Related notes
- [[../../Lessons/React/React - Lesson 07 - Server Components and React Internals]]
- [[../../Exercises/React/React - Exercise 07 - Server vs Client Boundary]]
- [[../../Concepts/React/React - Reconciliation, Keys, and Fiber]]
- [[../../Concepts/React/React - Rendering and Re-rendering]]

## Sources
- User-provided React conversation transcript from 2026-04-11.
- React blog: [React v18](https://react.dev/blog/2022/03/29/react-v18)
- React docs: [React DOM Server APIs](https://react.dev/reference/react-dom/server)
