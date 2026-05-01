---
type: run-report
skill: react/component
date: 2026-05-01
status: pass
component: PressButtonLink
output: runestone/src/components/PressButtonLink.tsx
---

# react/component — PressButtonLink

## Summary

- Component: `PressButtonLink`
- Primitive: native `<a>` element
- Props: `PressButtonLinkProps`
- Lines: `24`
- Output: `runestone/src/components/PressButtonLink.tsx`

## Spec conformance

- Followed ADR D1 by creating a separate `PressButtonLink` component
  instead of using `asChild` polymorphism.
- Rendered a native `<a>` element directly because Base UI has no Anchor
  primitive.
- Did not import or use any Base UI primitive, Radix Slot, `asChild`, or
  react-aria hooks in `PressButtonLink.tsx`.
- Exported `pressButtonVariants` from `PressButton.tsx` and imported it
  into `PressButtonLink.tsx` so both components share the same CVA variants.
- Defined `PressButtonLinkProps` as an interface extending
  `React.ComponentProps<'a'>` and
  `VariantProps<typeof pressButtonVariants>`.
- Used `cn()` to merge the shared CVA output with consumer `className`.

## Verification

- `pnpm exec tsc --noEmit` in `runestone/`: pass, exit code `0`.
- Static search found no `asChild`, Slot, Radix, react-aria hooks, or Base UI
  primitive import in `PressButtonLink.tsx`.

## Final status

Pass. `PressButtonLink` was produced at the requested path and follows the
native anchor exception documented by the Press component architecture ADR.
