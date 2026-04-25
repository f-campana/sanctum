> Superseded by PressButton v2. Retained as architectural
> evidence that informed the component architecture ADR.

# react/component — PressButton — 2026-04-25

Result: PASS

Inputs:
- `design_contract`: `runestone/DESIGN_RUNESTONE.md`
- `output_path`: `runestone/src/components/PressButton.tsx`

Report:
- Component: `PressButton`
- Props: `PressButtonProps`
- State: React Aria interaction state via `useButton`, `useHover`, and `useFocusRing`
- Composition pattern: CVA variants + Radix `Slot` `asChild` + React Aria `mergeProps`
- Lines: `208`

Checks:
- Functional component only: pass
- Named export for component and props interface: pass
- Variant model uses `variant: 'primary' | 'ghost'` and CVA: pass
- Native button prop surface via `React.ComponentProps<'button'>`: pass
- `asChild` polymorphism via Radix `Slot`: pass
- Built on React Aria `useButton`: pass
- Press token rules applied: 2px borders, 0 radius, JetBrains Mono 9px, uppercase, no box-shadow: pass
- Interaction state exposed through `data-*`: pass

Violations found:
- Draft implementation allowed React Aria to inject the native `disabled` attribute on the default button path, which violated the component spec requiring `aria-disabled` without removing the control from tab order. Corrected before the final file by stripping the injected `disabled` prop and preserving `aria-disabled`.

Remaining violations:
- None.
