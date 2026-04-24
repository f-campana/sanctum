---
type: lesson
status: draft
updated: 2026-04-11
tags:
  - react
  - architecture
  - frontend
---

# React - Lesson 04 - Advanced Patterns at Scale

## Why it matters
Small component decisions become architectural decisions at scale. This is where composition, controlled APIs, and state modeling either keep the system flexible or bury it in configuration props.

## Explanation
### Inversion of control
If the component author tries to anticipate every variation, the API grows into prop explosion. Better APIs hand structure back to the consumer.

The author should own behavior, state transitions, and constraints. The consumer should own layout, content, and composition.

### Compound components
Compound components split behavior across a set of related children that share internal state through context.

This is the pattern behind accordions, tabs, menus, and the kind of table API where the root owns selection, sorting, and editing while the consumer decides how the header and body are assembled.

### Controlled vs uncontrolled APIs
A controlled component lets the parent own the value and change handler. An uncontrolled component keeps the working value internally and only notifies the parent when needed.

The right choice depends on ownership. Controlled APIs are easier to synchronize across the tree; uncontrolled APIs are simpler when the component can manage itself.

### State machines
When a UI has distinct modes, use a state machine or reducer instead of many booleans. It keeps impossible states out of the model.

This is especially useful for loading, error, retry, editing, and commit flows where combinations like "loading and failed and successful" do not make sense.

### Colocation
Keep related behavior near the component that uses it. That includes state, styles, types, and tests when possible.

The farther apart related code lives, the more context switching and accidental drift you introduce.

## Examples
```tsx
<Accordion>
  <Accordion.Item>
    <Accordion.Trigger>Section 1</Accordion.Trigger>
    <Accordion.Content>Content</Accordion.Content>
  </Accordion.Item>
</Accordion>
```

The consumer controls structure while the accordion keeps the open/close logic.

```tsx
type FetchState =
  | { status: 'idle' }
  | { status: 'loading' }
  | { status: 'error'; error: Error }
  | { status: 'success'; data: unknown };
```

This prevents the "loading and error at the same time" class of bugs.

## Common misconceptions
- "More props always means a more flexible component."
- "Context is only for global app state."
- "A reducer is only for large apps."
- "Controlled and uncontrolled are interchangeable details."
- "Compound components are only a styling choice."

## Recap
At scale, React architecture is mostly about choosing ownership boundaries: who controls structure, who controls state, and how much of the implementation leaks into the API.

## Link to exercises
- [[../../Exercises/React/React - Exercise 04 - Refactor Prop Explosion]]

## Related concepts
- [[../../Concepts/React/React - Composition, Lifting State, and Controlled vs Uncontrolled]]

## Sources
- User-provided React conversation transcript from 2026-04-11.
