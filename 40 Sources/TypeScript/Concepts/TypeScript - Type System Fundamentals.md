---
type: concept
status: evergreen
updated: 2026-04-12
tags:
  - typescript
  - fundamentals
  - type-system
---

# TypeScript - Type System Fundamentals

## Summary
TypeScript is a compile-time checker that erases its types before runtime. It uses structural typing, so compatibility is about shape, not declared name. The core beginner-to-senior skills are understanding `any` vs `unknown`, type widening, narrowing, unions, intersections, generics, and the few places where TypeScript deliberately emits runtime code.

## Core idea
The compiler does not add runtime semantics. It observes JavaScript code and proves as much as it can before the program runs. Every useful TypeScript mental model follows from that boundary.

## Key rules
- Types exist at compile time and disappear from emitted JavaScript.
- `any` turns off checking; `unknown` keeps checking on until you narrow.
- Structural typing means "has the required shape" is enough.
- Object literals passed directly get excess property checks.
- `let` tends to widen, `const` preserves literal values for standalone bindings, and `as const` preserves literals deeply.
- Runtime checks only work with values that survive erasure, such as `typeof`, `instanceof`, and property checks.
- Interfaces can merge; type aliases do not.
- Enums emit runtime code, so they are the main exception to erasure.
- Unions mean "one of these"; intersections mean "all of these."
- Discriminated unions model state machines, and `never` helps with exhaustiveness checks.
- Type guards and assertion functions narrow from runtime checks.
- Generics preserve relationships between inputs and outputs.
- `keyof` gives you valid keys; indexed access gives you the value type for a key.
- `Object.keys()` is conservative because runtime objects may have more keys than the static type promises.
- Some TypeScript features are deliberately unsound for ergonomics: array covariance, `any` absorption, broad assertions, and parameter bivariance when strict checking is off.

## Common mistakes
- Treating type names as runtime values.
- Treating `any` and `unknown` as interchangeable.
- Assuming `const` deep freezes object properties.
- Assuming interfaces and type aliases have the same merging behavior.
- Forgetting that enums survive into JavaScript output.
- Confusing a union with "all properties shared by both branches."
- Using optional fields where a discriminated union would prevent impossible states.
- Forgetting to make switches exhaustive with `never`.
- Using `any` when `unknown` plus narrowing would be safer.
- Reaching for `as` before proving the runtime shape.
- Assuming object literals and variables are checked the same way.
- Assuming TypeScript is perfectly sound in every corner.

## Related notes
- [[../../Lessons/TypeScript/TypeScript - Lesson 01 - Foundations - Erasure, Structural Typing, and Narrowing]]
- [[../../Concepts/TypeScript/TypeScript - Narrowing, Discriminated Unions, and Exhaustiveness]]
- [[../../Lessons/TypeScript/TypeScript - Lesson 02 - Generics, keyof, and Utility Types]]
- [[../../Exercises/TypeScript/TypeScript - Exercise 01 - Trace Narrowing and Excess Property Checks]]
- [[../../Exercises/TypeScript/TypeScript - Exercise 02 - Preserve Relationships with Generics]]
- [[../../Exercises/TypeScript/TypeScript - Exercise 05 - Model a Discriminated Union State Machine]]

## Sources
- [[../../../40 Sources/Notes Imports/TypeScript - Claude Conversation - TypeScript Mastery]]
