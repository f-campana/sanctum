---
type: lesson
status: draft
updated: 2026-04-12
tags:
  - typescript
  - staff
  - principal
---

# TypeScript - Lesson 04 - Staff and Principal - Branding, Validation, Compiler Boundaries, and API Design

## Why it matters
This is where TypeScript turns into system design. You are no longer just writing types; you are deciding where trust enters the program, how public APIs should feel, and how much complexity the compiler should have to carry.

## Explanation
### Branded types
Structural typing is convenient, but it can mix up values that should never be interchangeable.

```ts
type Brand<T, B extends string> = T & { readonly __brand: B };

type UserId = Brand<string, "UserId">;
type OrderId = Brand<string, "OrderId">;
```

Branding adds a phantom distinction that exists only at compile time. That makes the boundary explicit.

### Runtime validation
TypeScript cannot prove that `response.json()` matches your types. You need runtime validation at the edge.

The practical pattern is:
- receive `unknown`
- validate it
- brand or refine it
- trust it internally

That validation can be handwritten, but schema libraries make it much easier to keep the runtime check and the static type in sync.

```ts
import { z } from "zod";

const UserSchema = z.object({
  id: z.string(),
  role: z.union([z.literal("admin"), z.literal("member")]),
});

const result = UserSchema.safeParse(await response.json());
if (!result.success) {
  throw new Error("Invalid payload");
}
```

When the schema is the source of truth, you can derive the TypeScript type from it instead of maintaining a separate interface by hand.

```ts
type User = z.infer<typeof UserSchema>;
```

That keeps validation and inference tied to the same definition.

### `satisfies`
`satisfies` checks that a value fits a type without widening away useful literal information.

```ts
const colors = {
  red: [255, 0, 0],
  green: "#00ff00",
} satisfies Record<string, string | [number, number, number]>;
```

That gives you validation plus narrow inference. If you want deeply literal values too, add `as const` separately.

### Unsound corners
TypeScript has deliberate escape hatches: `any`, assertions, array covariance, and broad index signatures. These exist for compatibility, but they are not free.

Other common unsound corners include `any` absorbing unions, parameter bivariance when strict function types are off, and double assertions through `unknown`.

```ts
const value = "hello" as unknown as number;
```

That pattern should stay rare and explicit.

### Module augmentation and compiler boundaries
Interfaces can merge, so library types can be augmented.

```ts
declare module "express" {
  interface Request {
    tenantId: string;
  }
}
```

That pattern depends on the compiler understanding declarations as open shapes, not closed records.

### Compiler pipeline and build tools
TypeScript flows through scanner, parser, binder, checker, and emitter. Fast build tools often stop after parsing and printing because they only need to erase types.

`isolatedDeclarations` pushes exported types toward explicit annotations so declaration emit can be more syntactic and less dependent on checker inference.

In practice that means exported functions and values need to be more explicit if you want declaration emit to be tool-friendly.

It does not change emit behavior by itself, and some patterns still need workarounds, so it is a constraint to adopt deliberately rather than a magic speed switch.

The practical shape of the pipeline matters:

- scanner: turns characters into tokens
- parser: turns tokens into an AST
- binder: builds symbols and scopes
- checker: infers, narrows, and reports type errors
- emitter: strips types and writes JavaScript or declaration files

That separation is why fast tools can skip the checker for builds but still rely on `tsc` for full validation.

### API design
Design public TypeScript APIs for inference and readability.

- Prefer inference-friendly signatures.
- Use overloads when the common cases deserve the clearest surface.
- Use conditional return types when the type relationship is genuinely generic.
- Use builders when the call must be staged.
- Keep error messages readable.

For example, a builder can encode staged state without forcing callers to remember ordering rules:

```ts
class QueryBuilder<TFrom extends string = never> {
  from<T extends string>(table: T): QueryBuilder<T> {
    return new QueryBuilder<T>();
  }

  execute(): TFrom extends never ? never : string {
    return "ok" as any;
  }
}
```

If the shape is broad but the common cases are clear, overloads usually produce better call-site errors than one giant conditional type.

```ts
function createElement(tag: "div"): HTMLDivElement;
function createElement(tag: "span"): HTMLSpanElement;
function createElement<T extends keyof HTMLElementTagNameMap>(
  tag: T
): HTMLElementTagNameMap[T];
```

That pattern gives clear common cases and a generic fallback.

### HKT workarounds
TypeScript does not have native higher-kinded types, so libraries simulate them with registries and defunctionalization.

That is powerful, but it is a library-design technique, not a default application pattern.

The common workaround is a registry keyed by a string literal:

```ts
interface URItoKind<A> {
  Array: Array<A>;
  Option: Option<A>;
}

type Kind<URI extends keyof URItoKind<any>, A> = URItoKind<A>[URI];
```

That lets a library talk about "the container" without native higher-kinded type support.

For most application code, this is a library-design curiosity rather than a daily need.

### Staff-level limits
Type-level arithmetic and string parsing are possible but should be used sparingly. Tuple-length arithmetic can express small counts, and template-literal parsing can derive route parameters or event names, but recursion depth and union size affect compiler performance.

```ts
type TupleOfLength<N extends number, T extends any[] = []> =
  T["length"] extends N ? T : TupleOfLength<N, [...T, any]>;

type Add<A extends number, B extends number> =
  [...TupleOfLength<A>, ...TupleOfLength<B>]["length"];

type ParseParams<T extends string> =
  T extends `${string}:${infer Param}/${infer Rest}`
    ? { [K in Param]: string } & ParseParams<`/${Rest}`>
    : T extends `${string}:${infer Param}`
      ? { [K in Param]: string }
      : {};
```

For expensive type experiments, `tsc --generateTrace` can help you see where the checker is spending time.

## Examples
```ts
function createUserId(raw: string): UserId {
  return raw as UserId;
}
```

```ts
function loadUser(input: unknown) {
  // validate input here, then trust the validated result
}
```

```ts
type Reader<out T> = { get(): T };
type Writer<in T> = { set(value: T): void };
```

## Common misconceptions
- "A branded type changes runtime behavior."
- "A type assertion is the same thing as validation."
- "A fast transpiler also performs full type checking."
- "An overloaded API is always worse than a generic one."
- "The compiler pipeline is only relevant to TypeScript internals."

## Recap
Staff and principal-level TypeScript is about boundaries, trust, and API shape. Use brands and runtime validation at the edge, use `satisfies` to preserve useful inference, and design public types for humans first.

## Link to exercise(s)
- [[../../Exercises/TypeScript/TypeScript - Exercise 04 - Model a Safe Boundary]]

## Related concepts
- [[../../Concepts/TypeScript/TypeScript - Runtime Boundaries and Safety]]
- [[../../Concepts/TypeScript/TypeScript - Compiler and API Design]]

## Sources
- [[../../../40 Sources/Notes Imports/TypeScript - Claude Conversation - TypeScript Mastery]]
