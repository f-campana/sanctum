---
type: concept
status: evergreen
updated: 2026-04-12
tags:
  - typescript
  - narrowing
  - unions
  - control-flow
---

# TypeScript - Narrowing, Discriminated Unions, and Exhaustiveness

## Summary
TypeScript narrows union types by following control flow and runtime checks. Discriminated unions use a shared literal field to model real state machines, and exhaustiveness checks with `never` make future cases impossible to forget.

## Core idea
Runtime checks only help TypeScript when the check uses a JavaScript value that still exists after erasure. A good discriminant gives the compiler a stable way to narrow the branch, and a `never` check tells you when you missed a state.

## Key rules
- `typeof`, `instanceof`, `in`, equality checks, and truthiness are all runtime checks TypeScript understands.
- A discriminated union needs a shared property, literal values, and one distinct literal per branch.
- Narrowing by elimination works when a branch returns or throws, but it is easy to forget a new union member.
- Type guards use a `value is Type` return type and narrow inside an `if` branch.
- Assertion functions use `asserts value is Type` and narrow from the call onward.
- `never` represents an impossible branch and is useful for exhaustive switches.

## Common mistakes
- Modeling state with a single interface full of optional fields.
- Expecting interface names to exist at runtime.
- Writing a guard that is too complex to trust.
- Relying on fallthrough logic instead of an explicit exhaustive check.
- Forgetting that TypeScript trusts user-defined guards and assertions.

## Related notes
- [[../../Lessons/TypeScript/TypeScript - Lesson 01 - Foundations - Erasure, Structural Typing, and Narrowing]]
- [[../../Exercises/TypeScript/TypeScript - Exercise 05 - Model a Discriminated Union State Machine]]
- [[../../Concepts/TypeScript/TypeScript - Type System Fundamentals]]

## Sources
- [[../../../40 Sources/Notes Imports/TypeScript - Claude Conversation - TypeScript Mastery]]
