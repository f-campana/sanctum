---
type: lesson
status: draft
updated: 2026-04-12
tags:
  - typescript
  - advanced-types
  - templates
---

# TypeScript - Lesson 03 - Advanced Type Programming - Conditional Types, infer, Variance, and Template Literals

## Why it matters
This is the point where TypeScript becomes a type-level programming language. The compiler is no longer just checking your annotations; it is transforming types for you.

## Explanation
### Conditional types
Conditional types are the type-level version of `if`.

```ts
type IsString<T> = T extends string ? "yes" : "no";
```

When the checked type is a naked type parameter, the condition distributes over unions.

```ts
type Result = IsString<string | number>; // "yes" | "no"
type NoDistribute<T> = [T] extends [string] ? "yes" : "no";
type Result2 = NoDistribute<string | number>; // "no"
```

Wrap the type in a tuple to stop distribution.

### `infer`
`infer` captures a piece of a matched type.

```ts
type ReturnTypeOf<T> = T extends (...args: any[]) => infer R ? R : never;
type FirstArg<T> = T extends (first: infer F, ...rest: any[]) => any ? F : never;
type Element<T> = T extends (infer E)[] ? E : never;
```

This is how the compiler can "pattern match" on function, array, and promise shapes.

One subtle edge case: a function with no parameters can still match a pattern like `T extends (first: infer F, ...rest: any[]) => any`. TypeScript can prove the function is assignable, but there is no concrete first argument to extract, so the inferred type falls back to `unknown`.

### Recursive conditional types
You can recurse to peel layers.

```ts
type UnwrapPromise<T> = T extends Promise<infer U> ? UnwrapPromise<U> : T;
```

### Mapped types and key remapping
Mapped types iterate over keys and rebuild an object type.

```ts
type Getters<T> = {
  [K in keyof T as `get${Capitalize<string & K>}`]: () => T[K];
};
```

### Variance
Variance answers whether `Container<Dog>` can stand in for `Container<Animal>`.

- Output positions are covariant.
- Input positions are contravariant.
- Both positions together make the type invariant.

Arrays are intentionally unsound in TypeScript for ergonomics. Function parameters are contravariant under `strictFunctionTypes`.

In newer TypeScript versions, you can also write `in`, `out`, or `in out` on type parameters to document or enforce variance in complex generic helpers.

```ts
type Reader<out T> = { get(): T };
type Writer<in T> = { set(value: T): void };
type Mapper<T> = (input: T) => T;
```

`Mapper<T>` is invariant because `T` appears in both input and output positions.

### Overloads vs conditional return types
Use overloads when you want explicit call signatures and clear public-facing errors. Use conditional return types when the return type needs to flow from generic input and the API is internal or highly compositional.

One practical cost of conditional return types is that the implementation body often does not narrow cleanly against the conditional return annotation, so you may need an assertion inside the function even when the call site looks perfectly typed.

```ts
function parse(input: string): number;
function parse(input: number): string;
function parse(input: string | number): string | number {
  return typeof input === "string" ? input.length : String(input);
}
```

Overloads usually read better at the public API boundary, while conditional return types compose better with generics.

### Template literal types
Template literals let you compute string unions and parse string shapes.

```ts
type EventName = `on${Capitalize<"click" | "focus">}`; // "onClick" | "onFocus"
type Split<S extends string, D extends string> =
  S extends `${infer Head}${D}${infer Tail}` ? [Head, ...Split<Tail, D>] : [S];
```

This is compile-time string manipulation, not runtime string processing.

TypeScript also ships intrinsic string helpers for template-literal work: `Uppercase`, `Lowercase`, `Capitalize`, and `Uncapitalize`.

Large unions can expand combinatorially when used in template literals, so keep string unions bounded when possible.

## Examples
```ts
type Handlers<T> = {
  [K in keyof T as `on${Capitalize<string & K>}`]: (event: T[K]) => void;
};

type Events = {
  click: { x: number; y: number };
  blur: {};
};
```

```ts
type Mapper<T> = (input: T) => T;
```

`Mapper<T>` is invariant because `T` appears in both input and output positions.

## Common misconceptions
- "Conditional types always collapse unions into one branch."
- "`infer` can extract anything anywhere."
- "Arrays are sound because TypeScript accepted the assignment."
- "Overloads and conditional return types are just stylistic alternatives."
- "Template literal types are runtime strings with extra metadata."

## Recap
Once you understand distribution, extraction, variance, and string templates, you can read most advanced helper types as ordinary shape transformations.

## Link to exercise(s)
- [[../../Exercises/TypeScript/TypeScript - Exercise 03 - Conditional Types, infer, and Template Literals]]

## Related concepts
- [[../../Concepts/TypeScript/TypeScript - Type-Level Programming]]
- [[../../Concepts/TypeScript/TypeScript - Compiler and API Design]]

## Sources
- [[../../../40 Sources/Notes Imports/TypeScript - Claude Conversation - TypeScript Mastery]]
