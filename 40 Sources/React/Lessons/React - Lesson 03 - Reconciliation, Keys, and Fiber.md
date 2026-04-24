---
type: lesson
status: draft
updated: 2026-04-11
tags:
  - react
  - fiber
  - reconciliation
---

# React - Lesson 03 - Reconciliation, Keys, and Fiber

## Why it matters
Render only tells React what the UI should look like. Reconciliation decides what to keep, what to update, and what to discard.

## Explanation
### Identity rules
React uses element type and key to decide whether two UI descriptions represent the same logical instance.

The position in the tree also matters. React preserves state when the same component appears at the same position with the same identity. Change the type or move identity around without a stable key, and state resets.

### State preservation
Same type and same key usually preserve state. Different type at the same position usually destroys state.

That is why toggling between `<Profile />` and `<Settings />` at the same slot destroys the old branch's state. If you want both branches to survive, you either keep them mounted, lift the state up, or give each branch a stable identity in a way React can preserve.

### Why keys matter
Keys are not a list-only detail. They are the identity handle React uses when sibling order changes.

Without keys, React falls back to sibling position. With keys, React can see that items moved rather than disappeared.

### Fiber
Fiber is React's bookkeeping layer. It keeps a work-in-progress tree, the current tree, and the pointers needed to walk the tree without recursion.

That double-buffering is what makes concurrent rendering possible. React can build the next tree without mutating the current one until commit.

## Examples
```tsx
function App({ showProfile }) {
  return showProfile ? <Profile /> : <Settings />;
}
```

Switching between `Profile` and `Settings` at the same position destroys the old branch's local state.

```tsx
{items.map((item) => (
  <Row key={item.id} item={item} />
))}
```

Stable keys let React keep each row's identity across reorders and insertions.

## Common misconceptions
- "Keys are only for array rendering."
- "React diffing is a complete tree comparison."
- "State follows whatever is visually on screen."
- "Fiber is just an implementation detail with no teaching value."

## Recap
Identity is the central reconciliation question. Once you know how React matches old and new elements, state loss, state preservation, and list bugs become much easier to predict.

## Link to exercises
- [[../../Exercises/React/React - Exercise 03 - Keys, Identity, and State Preservation]]

## Related concepts
- [[../../Concepts/React/React - Reconciliation, Keys, and Fiber]]

## Sources
- User-provided React conversation transcript from 2026-04-11.
