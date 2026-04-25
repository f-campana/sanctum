> Superseded by PressButton v2. Retained as architectural
> evidence that informed the component architecture ADR.

# typescript/component — PressButton — 2026-04-25

Result: PASS

Report:
- File: `runestone/src/components/PressButton.tsx`
- Violations: `0`
- Rules applied: `strict`, `exactOptionalPropertyTypes`, `noUncheckedIndexedAccess`, exported props interface, no `any`, `React.ReactNode` children, CVA variant union, documented runtime-safe casts

Project validation:
- `runestone/tsconfig.json` was missing explicit `exactOptionalPropertyTypes` and `noUncheckedIndexedAccess`. Corrected before final validation.
- `runestone` did not have a local `typescript` binary. Corrected before final validation by adding `typescript` as a dev dependency.

File validation:
- Prop interface is explicit and exported: pass
- No `any` in the component surface: pass
- `children` uses `React.ReactNode`: pass
- `variant` and `size` are explicit unions: pass
- `isDisabled` is a dedicated boolean state prop, not a variant boolean: pass
- Runtime casts are limited and documented where needed: pass

Corrections made before the final file:
- Narrowed the slotted element type for `useButton`.
- Normalized the button `value` before passing it into React Aria.
- Split React Aria hook inputs from DOM-only props to satisfy `exactOptionalPropertyTypes`.
- Documented and constrained the ref and `disabled` stripping casts.

Validation command:
```bash
pnpm -C runestone exec tsc --noEmit
```

Remaining violations:
- None.
