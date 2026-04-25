---
type: run-report
skill: react/component
date: 2026-04-26
status: pass
component: PressButton
output: runestone/src/components/PressButton.tsx
---

# react/component — PressButton v2

## Summary

- Component: `PressButton`
- Primitive: `ButtonPrimitive` from `@base-ui-components/react/button`
- Props: `PressButtonProps`
- Lines: `58`
- Output: `runestone/src/components/PressButton.tsx`

## Spec conformance

- Followed the Press component template from the ADR: Base UI primitive, CVA variants, `cn()` merge, named props export, and prop spread.
- Kept the component button-only. No `asChild`, no Slot, no react-aria hooks.
- Encoded Press inviolable rules in the base class string: `border-2 border-solid rounded-none shadow-none`.
- Used CSS pseudo-classes only for interaction states: `enabled:hover:*`, `enabled:active:*`, `focus-visible:*`, `disabled:*`.
- Implemented the requested variants:
  - `primary`: dark fill with orange hover.
  - `ghost`: transparent with orange border and orange text on hover.
- Applied the requested typography: JetBrains Mono via `font-mono`, `text-[9px]`, `tracking-[0.1em]`, `uppercase`.

## Supporting changes

- Installed `@base-ui-components/react@1.0.0-rc.0`.
- Added `runestone/src/lib/utils.ts` with `cn()` using `clsx` and `tailwind-merge`.
- Added `@/* -> ./src/*` alias support in `runestone/tsconfig.json` and `runestone/astro.config.mjs` so the ADR template import path resolves.

## Final status

Pass. `PressButton` was produced at the requested path and follows the current Press ADR structure.
