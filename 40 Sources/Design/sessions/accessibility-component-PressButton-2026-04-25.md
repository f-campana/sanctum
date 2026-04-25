> Superseded by PressButton v2. Retained as architectural
> evidence that informed the component architecture ADR.

# accessibility/component — PressButton — 2026-04-25

Result: PASS

Report:
- Component: `PressButton`
- Widget type: `button`
- Violations: `0`
- APG keyboard model: `pass`

Checks:
- Native button element is the default render path: pass
- React Aria `useButton` is used as the behavioral primitive: pass
- `Enter` and `Space` activation are delegated to React Aria: pass
- Focus ring is keyboard-only via `data-focus-visible`: pass
- `aria-disabled` is used instead of the HTML `disabled` attribute: pass
- Interaction state is surfaced via `data-hovered`, `data-pressed`, `data-focused`, `data-focus-visible`, and `data-disabled`: pass
- Focus indicator matches the Press rule: `2px` outline with `2px` offset using `--pr-focus-ring`: pass

Violations found:
- Draft implementation still allowed the native `disabled` attribute to leak onto the button element through React Aria. Corrected before final file write so disabled buttons remain focusable and expose `aria-disabled`.

Notes:
- No runtime assistive technology test was performed. This report covers structural and keyboard-contract validation only.

Remaining violations:
- None.
