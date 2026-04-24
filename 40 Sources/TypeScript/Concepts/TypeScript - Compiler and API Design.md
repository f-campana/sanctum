---
type: concept
status: evergreen
updated: 2026-04-12
tags:
  - typescript
  - compiler
  - api-design
---

# TypeScript - Compiler and API Design

## Summary
TypeScript is built as a scanner, parser, binder, checker, and emitter pipeline. That architecture explains why some tools can strip types quickly, why declaration emit has limits, and why public APIs should be designed for inference and readable errors.

## Core idea
Good TypeScript API design follows the compiler's strengths. Make inference easy, keep signatures readable, and avoid forcing callers to specify types manually unless there is no better option.

## Key rules
- Parsing and type checking are separate problems.
- Fast build tools often skip the checker and only strip syntax.
- `isolatedDeclarations` requires explicit export annotations so declaration emit can be purely syntactic.
- Higher-kinded types are not native, so registry or defunctionalization patterns are used instead.
- Builder patterns can encode staged type state.
- Overloads are often better for public-facing call sites; conditional return types are often better for internal composition.
- Error messages are part of the API.
- Recursive, union-heavy, or deeply nested type helpers can slow the checker and the editor.
- `tsc --generateTrace` is useful when a type helper feels suspiciously expensive.

## Common mistakes
- Assuming a fast transpiler also performs full type checking.
- Requiring callers to write generic arguments by hand.
- Hiding complexity inside one huge conditional type.
- Shipping public types that are technically clever but hard to read.
- Forgetting that editor performance is part of API quality.
- Ignoring how type complexity affects inference and hover latency.
- Treating `isolatedDeclarations` as a runtime or emit optimization instead of a declaration-typing constraint.

## Related notes
- [[../../Lessons/TypeScript/TypeScript - Lesson 04 - Staff and Principal - Branding, Validation, Compiler Boundaries, and API Design]]
- [[../../Lessons/TypeScript/TypeScript - Lesson 03 - Advanced Type Programming - Conditional Types, infer, Variance, and Template Literals]]

## Sources
- [[../../../40 Sources/Notes Imports/TypeScript - Claude Conversation - TypeScript Mastery]]
