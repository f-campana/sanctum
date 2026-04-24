---
type: concept
status: evergreen
updated: 2026-04-12
tags:
  - typescript
  - safety
  - runtime-boundary
---

# TypeScript - Runtime Boundaries and Safety

## Summary
TypeScript only protects the code it can see at compile time. When data arrives at runtime, you need validation before you can trust it. Branded types, `satisfies`, module augmentation, and careful use of `unknown` help keep the trusted interior separate from untrusted input.

## Core idea
The dangerous boundary is where raw JavaScript data enters your program. Validate there, brand the result if needed, and let the rest of the codebase assume the refined type is real.

## Key rules
- Validate external data at the edge of the system.
- Use schemas or guards to turn `unknown` into trusted data.
- Use branded types to stop semantically distinct values from mixing.
- Use `satisfies` when you want validation without widening the inferred type.
- Treat `any` and broad assertions as deliberate escape hatches, not defaults.
- Prefer interface-based declaration merging when you need to augment a library type.
- Keep recursive or union-heavy types manageable so the compiler stays responsive.
- Schema-first validation is usually cleaner than maintaining separate runtime checks and static types by hand.

## Common mistakes
- Trusting `response.json()` without validation.
- Using `as User` as if it were a runtime check.
- Thinking branded types exist at runtime.
- Using `any` to avoid modeling the boundary.
- Writing type-level machinery that slows the editor for everyone else.
- Forgetting that `satisfies` validates shape but does not replace runtime validation.

## Related notes
- [[../../Lessons/TypeScript/TypeScript - Lesson 04 - Staff and Principal - Branding, Validation, Compiler Boundaries, and API Design]]
- [[../../Exercises/TypeScript/TypeScript - Exercise 04 - Model a Safe Boundary]]
- [[../../Lessons/TypeScript/TypeScript - Lesson 03 - Advanced Type Programming - Conditional Types, infer, Variance, and Template Literals]]

## Sources
- [[../../../40 Sources/Notes Imports/TypeScript - Claude Conversation - TypeScript Mastery]]
