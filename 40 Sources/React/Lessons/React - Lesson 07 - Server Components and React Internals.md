---
type: lesson
status: draft
updated: 2026-04-11
tags:
  - react
  - server-components
  - internals
---

# React - Lesson 07 - Server Components and React Internals

## Why it matters
These two areas show where the React mental model extends beyond the browser: across the server/client boundary and into the implementation that makes the earlier lessons possible.

## Explanation
### Server Components
Server Components let data-heavy, non-interactive UI run on the server so the client bundle stays smaller. Client Components keep state, events, and browser APIs.

Server Components can `await` data during render. Client Components opt in with `'use client'` and carry the interactive surface.

### Boundary rule
A Server Component can render a Client Component, but a Client Component cannot import Server Component code directly.

Server Components are serialized into a payload that the client reconciler can consume. The point is not just "HTML from the server" but "a tree the client can continue reconciling."

That means you can compose server-rendered children inside client wrappers when you need interactivity around static content.

### Internals
Fiber, the scheduler, the hooks list, and the work loop are the structures that make render interruption, reconciliation, and state preservation possible.

The important source-code landmarks are:
- `ReactFiberHooks.js` for the hook list and mount/update dispatchers
- `ReactFiberWorkLoop.js` for the cooperative work loop and yielding
- `ReactFiberBeginWork.js` for reconciliation entry points
- the scheduler package for time slicing and task priorities

The scheduler cooperates with the browser by posting work through message-based tasks and checking `shouldYield()` so React can pause before a frame gets too expensive.

Those structures explain why React can pause, resume, and restart work without losing state identity.

They also explain why hooks are positional, why `memoizedState` lives on the fiber, and why the render phase can be abandoned without touching the DOM.

### Why this matters practically
If you understand the internals, React behavior stops feeling arbitrary. You can reason about identity, scheduling, and state preservation from first principles.

## Examples
```tsx
// Server Component
async function BlogPost({ id }) {
  const post = await db.posts.findUnique({ where: { id } });
  return <article>{post.title}</article>;
}
```

```tsx
'use client';
function LikeButton() {
  const [liked, setLiked] = useState(false);
  return <button onClick={() => setLiked(!liked)}>{liked ? '♥' : '♡'}</button>;
}
```

## Common misconceptions
- "Server Components are just SSR with a new name."
- "Client Components can freely import anything."
- "Internals are only for library authors."
- "There is a `use server` directive for ordinary Server Components."

## Recap
Server Components move work to the server. Internals explain why the earlier React rules work the way they do.

## Link to exercises
- [[../../Exercises/React/React - Exercise 07 - Server vs Client Boundary]]

## Related concepts
- [[../../Concepts/React/React - Reconciliation, Keys, and Fiber]]
- [[../../Concepts/React/React - Rendering and Re-rendering]]
- [[../../Concepts/React/React - Server Components and Internals]]
- [[../../Concepts/React/React - Concurrent React, Suspense, and Transitions]]

## Sources
- User-provided React conversation transcript from 2026-04-11.
