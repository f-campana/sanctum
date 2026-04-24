---
type: concept
status: evergreen
updated: 2026-04-12
tags:
  - typescript
  - advanced-types
  - type-system
---

# TypeScript - Type-Level Programming

## Summary
Conditional types, `infer`, mapped types, key remapping, variance, and template literal types let TypeScript transform and inspect types. These tools make the type system feel like a small programming language.

## Core idea
The type checker can match against the shape of a type, extract parts of it, and rebuild a new type. Once you see that, built-in helpers like `Pick`, `Omit`, `ReturnType`, and `Parameters` stop looking magical.

## Key rules
- `T extends U ? X : Y` is the type-level `if`.
- Conditional types distribute over unions when the checked type is a naked type parameter.
- Wrap a type in a tuple to stop distribution.
- `infer` captures part of a matched type pattern.
- Mapped types iterate over keys.
- Key remapping with `as` can rename or filter keys.
- Variance depends on whether a type parameter appears in input position, output position, or both.
- Function parameters are contravariant under `strictFunctionTypes`, and arrays are intentionally covariant for ergonomics.
- `infer` only captures what actually matches the pattern; when there is nothing concrete to capture, TypeScript may fall back to `unknown`.
- Template literal types can generate and parse string unions.
- Newer TypeScript versions support `in`, `out`, and `in out` annotations for complex variance-sensitive helpers.
- Overloads are often better for user-facing APIs with a few distinct cases; conditional return types are often better when the output depends on a generic input.

## Common mistakes
- Forgetting that conditional types distribute over unions.
- Using `infer` where the pattern does not actually match.
- Building huge recursive or union-heavy types without considering compiler cost.
- Confusing overloads with conditional return types.
- Assuming template literal types are "just strings" and not compile-time unions.
- Building recursive helpers without considering checker cost.

## Related notes
- [[../../Lessons/TypeScript/TypeScript - Lesson 03 - Advanced Type Programming - Conditional Types, infer, Variance, and Template Literals]]
- [[../../Exercises/TypeScript/TypeScript - Exercise 03 - Conditional Types, infer, and Template Literals]]
- [[../../Lessons/TypeScript/TypeScript - Lesson 02 - Generics, keyof, and Utility Types]]

## Sources
- [[../../../40 Sources/Notes Imports/TypeScript - Claude Conversation - TypeScript Mastery]]
