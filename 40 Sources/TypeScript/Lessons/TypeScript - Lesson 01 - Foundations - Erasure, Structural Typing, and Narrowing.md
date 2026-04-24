---
type: lesson
status: draft
updated: 2026-04-12
tags:
  - typescript
  - fundamentals
---

# TypeScript - Lesson 01 - Foundations - Erasure, Structural Typing, and Narrowing

## Why it matters
This is the base mental model. If you confuse compile time with runtime, everything else in TypeScript feels arbitrary.

## Explanation
### Type erasure
TypeScript annotations are for the compiler, not the runtime.

```ts
function greet(name: string) {
  return `Hello ${name}`;
}
```

The `: string` exists for checking and disappears from the emitted JavaScript. That means you cannot branch on a pure TypeScript type at runtime.

Two important corollaries sit right beside that rule:

```ts
let value: any = "hello";
value = 42; // no checking
```

`any` turns off safety. `unknown` does the opposite: it keeps the value opaque until you narrow it. In practice, `unknown` is the safe default when data comes from outside your trusted code.

### Structural typing
TypeScript checks whether a value has the right shape.

```ts
interface Cat {
  name: string;
  meow(): void;
}

interface Dog {
  name: string;
  bark(): void;
}

function greetPet(pet: { name: string }) {
  console.log(pet.name);
}
```

Any value with a `name` property can be passed to `greetPet`, even if it was never declared as that interface.

That is why runtime checks must use values that still exist after compilation. `typeof` works because it is a JavaScript operator. `instanceof` works for classes because classes survive as constructor functions. But interface names disappear, so you cannot test `pet instanceof Cat` when `Cat` is only an interface.

### Interfaces, type aliases, and enums
Interfaces are open for declaration merging. Type aliases are closed.

```ts
interface User {
  id: string;
}

type UserId = string;
```

That distinction matters when you need to augment a library type. Enums are the main exception to type erasure because they emit runtime JavaScript. Most modern code prefers `as const` objects plus union literals when it wants named values without the enum-emitted runtime machinery.

`const enum` is the special case to remember: it inlines values instead of emitting the normal enum object, which is why it can be awkward with toolchains that rely on isolated module transforms.

### Excess property checks
Object literals passed directly are checked more strictly than variables.

```ts
greetPet({ name: "Milo", extra: true }); // error
const pet = { name: "Milo", extra: true };
greetPet(pet); // ok
```

That stricter check is a practical typo detector, not a different type system.

### Widening and narrowing
`let` usually widens, `const` preserves literal values for standalone bindings, and `as const` preserves literals deeply.

```ts
let a = "hello";   // string
const b = "hello"; // "hello"

const config = {
  host: "localhost",
  port: 3000,
} as const;
```

`as const` is a convenient way to keep literal values and readonly properties on object literals, but it does not turn runtime data into a compile-time type system feature. The object still exists at runtime.

TypeScript narrows through runtime checks:

```ts
function handle(value: string | number | null) {
  if (value === null) return;
  if (typeof value === "string") {
    return value.toUpperCase();
  }
  return value.toFixed(2);
}
```

The point is not just that the branches type-check. The point is that the compiler follows control flow and remembers what remains possible after each check.

### Discriminated unions and exhaustiveness
When a value represents a domain state, optional properties are usually too weak. A discriminated union gives each state its own branch.

```ts
type MortgageApplication =
  | { status: "draft"; applicantId: string }
  | { status: "submitted"; applicantId: string; submittedAt: Date }
  | { status: "approved"; applicantId: string; rate: number; approvedBy: string }
  | { status: "rejected"; applicantId: string; reason: string };
```

The shared `status` property is the discriminant. A `switch` or `if` on that field narrows to a single branch.

```ts
function handle(app: MortgageApplication) {
  switch (app.status) {
    case "approved":
      return app.rate;
    case "rejected":
      return app.reason;
    default:
      const _exhaustive: never = app.status;
      return _exhaustive;
  }
}
```

That `never` check is what catches future states when you forget to handle them.

### Type guards and assertion functions
TypeScript can narrow from runtime checks, but only if you express the check in a way the compiler understands.

```ts
function isApproved(
  app: MortgageApplication
): app is Extract<MortgageApplication, { status: "approved" }> {
  return app.status === "approved";
}

function assertSubmitted(
  app: MortgageApplication
): asserts app is Extract<MortgageApplication, { status: "submitted" }> {
  if (app.status !== "submitted") {
    throw new Error("Not submitted");
  }
}
```

Type guards narrow inside the `if` branch. Assertion functions narrow from the call onward. The compiler trusts both, so they should stay small and obvious.

### Unions and intersections
Unions mean "one of these". Intersections mean "all of these."

```ts
type A = { name: string };
type B = { age: number };

type OneOrTheOther = A | B;
type Both = A & B;
```

A union gives you less certainty about the current value, so you must narrow before reading branch-specific fields.

Think of types as sets of values: a union is a larger set, and an intersection is a smaller set. That is why a union gives you fewer guaranteed properties, while an intersection gives you more.

### What comes next
Generics, `keyof`, indexed access, and utility types are covered in the next lesson. The important bridge is that narrowing decides which branch of a union you are in, while generics preserve relationships once the shape is already known.

## Examples
```ts
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = { name: "Fabien", age: 30 };
const name = getProperty(user, "name"); // string
```

```ts
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};
```

## Common misconceptions
- "Types exist at runtime."
- "An interface name is a runtime tag."
- "`const` makes every nested property immutable."
- "A union lets me access everything from every branch."
- "Optional fields are good enough for every state machine."
- "A switch is exhaustive just because it looks complete."
- "The direct literal and the variable case are checked the same way."
- "Utility types are magic built-ins, not composable patterns."

## Recap
TypeScript is a static model over JavaScript. It checks shape, widens and narrows aggressively, and lets you model real state with discriminated unions, guards, and exhaustiveness checks instead of vague optional fields.

## Link to exercise(s)
- [[../../Exercises/TypeScript/TypeScript - Exercise 01 - Trace Narrowing and Excess Property Checks]]
- [[../../Exercises/TypeScript/TypeScript - Exercise 05 - Model a Discriminated Union State Machine]]

## Related concepts
- [[../../Concepts/TypeScript/TypeScript - Type System Fundamentals]]
- [[../../Concepts/TypeScript/TypeScript - Runtime Boundaries and Safety]]
- [[../../Concepts/TypeScript/TypeScript - Narrowing, Discriminated Unions, and Exhaustiveness]]

## Sources
- [[../../../40 Sources/Notes Imports/TypeScript - Claude Conversation - TypeScript Mastery]]
