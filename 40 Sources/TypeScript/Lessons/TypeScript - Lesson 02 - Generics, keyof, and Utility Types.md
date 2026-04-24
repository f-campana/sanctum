---
type: lesson
status: draft
updated: 2026-04-12
tags:
  - typescript
  - generics
  - utility-types
---

# TypeScript - Lesson 02 - Generics, keyof, and Utility Types

## Why it matters
This is where TypeScript stops being "annotations on top of JavaScript" and starts becoming a way to describe relationships between values and their types.

## Explanation
### Generics preserve relationships
Generics let you keep the caller's specific type instead of erasing it.

```ts
function first<T>(items: T[]): T | undefined {
  return items[0];
}
```

That is more useful than `unknown[] -> unknown` because the output keeps the exact element type.

If you want to guarantee a value exists, use a non-empty tuple or a separate runtime check.

The real reason to reach for a generic is to preserve a relationship. A type parameter that appears only once usually adds noise rather than value.

### Constraints narrow the possible input

```ts
function getLength<T extends { length: number }>(value: T): number {
  return value.length;
}
```

The constraint says what `T` must be allowed to use, while still preserving the exact subtype the caller passed.

### `keyof` and indexed access

```ts
type User = { name: string; age: number; email: string };

type UserKeys = keyof User; // "name" | "age" | "email"
type UserValues = User[keyof User]; // string | number
```

This is the basis for safe dynamic property access:

```ts
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}
```

Why does `Object.keys(user)` still come back as `string[]`? Because the runtime object may have more properties than the static type promises. Structural typing only guarantees the minimum shape, so TypeScript stays conservative when you inspect actual runtime keys.

```ts
type NameType = User["name"]; // string
type UserReturn = ReturnType<() => User>;
type UserParams = Parameters<(id: string, active: boolean) => void>;
```

`ReturnType` and `Parameters` are good examples of how the standard library builds useful helpers out of conditional types and `infer`.

### Utility types are composed types
`Pick`, `Omit`, `Readonly`, `Partial`, `Required`, `Exclude`, and `Extract` are all built from mapped types, indexed access, and conditional types.

```ts
type Pick<T, K extends keyof T> = {
  [P in K]: T[P];
};

type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};

type Partial<T> = {
  [P in keyof T]?: T[P];
};

type Required<T> = {
  [P in keyof T]-?: T[P];
};

type Omit<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>;
type PartialBy<T, K extends keyof T> = Omit<T, K> & Partial<Pick<T, K>>;
```

That means utility types are not a separate magic layer. They are examples of how the type system is wired together.

## Examples
```ts
function merge<A extends object, B extends object>(a: A, b: B): A & B {
  return { ...a, ...b };
}

const result = merge({ name: "Fabien" }, { age: 30 });
// result is { name: string } & { age: number }
```

```ts
type PartialBy<T, K extends keyof T> = Omit<T, K> & Partial<Pick<T, K>>;
```

## Common misconceptions
- "A generic is useful whenever I do not know the type."
- "A constraint replaces the need for a generic."
- "Utility types are special syntax rather than normal type composition."
- "Object.keys should be typed as the exact keys of the static type."
- "A type parameter that appears only once adds value."
- "A constraint and a generic are the same thing."

## Recap
Generics preserve relationships, `keyof` and indexed access inspect object shapes, and utility types are reusable compositions of the same primitives.

## Link to exercise(s)
- [[../../Exercises/TypeScript/TypeScript - Exercise 02 - Preserve Relationships with Generics]]

## Related concepts
- [[../../Concepts/TypeScript/TypeScript - Type System Fundamentals]]
- [[../../Concepts/TypeScript/TypeScript - Type-Level Programming]]

## Sources
- [[../../../40 Sources/Notes Imports/TypeScript - Claude Conversation - TypeScript Mastery]]
