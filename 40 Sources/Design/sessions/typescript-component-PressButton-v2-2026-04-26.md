---
type: run-report
skill: typescript/component
date: 2026-04-26
status: pass
file: runestone/src/components/PressButton.tsx
tsconfig: runestone/tsconfig.json
---

# typescript/component — PressButton v2

File: `runestone/src/components/PressButton.tsx`  
Violations found during validation: `3`  
Rules applied: `strict`, `exactOptionalPropertyTypes`, `noUncheckedIndexedAccess`, explicit props interface, no `any`, variant typing via CVA, exported props surface

## Violations found

### Rule: Compiler compatibility for alias-backed component import
Location: `runestone/tsconfig.json:4`
Found: `baseUrl` was added to support the ADR's `@/lib/utils` import, and TypeScript 6 refused to proceed without an explicit deprecation acknowledgement.
Required: Add `ignoreDeprecations: "6.0"` so the project can continue to typecheck while using the current path-alias mechanism.
Status: Corrected.

### Rule: Prop interface must extend a statically known object type
Location: `runestone/src/components/PressButton.tsx:37`
Found: `PressButtonProps` initially extended `ButtonPrimitive.Props`, but Base UI exports that type as a union, which TypeScript does not allow an interface to extend.
Required: Narrow the primitive surface to the native button branch before extending it from the component props interface.
Status: Corrected by extracting the native button props and omitting polymorphic members.

### Rule: Explicit props interface must expose valid component members
Location: `runestone/src/components/PressButton.tsx:41`
Found: Because the initial interface extension failed, `className` was not recognized on `PressButtonProps`.
Required: Rebuild the props interface from a valid object type and declare `className?: string` explicitly for the wrapper surface.
Status: Corrected.

## Final validation

- `runestone/tsconfig.json` includes `strict: true`, `exactOptionalPropertyTypes: true`, and `noUncheckedIndexedAccess: true`.
- `PressButtonProps` is exported.
- No `any` was introduced.
- Variant typing is driven by `VariantProps<typeof pressButtonVariants>`.
- `pnpm exec tsc --noEmit` passes.

## Final status

Pass. No remaining TypeScript violations.
