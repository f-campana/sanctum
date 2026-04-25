---
type: run-report
skill: accessibility/component
date: 2026-04-26
status: pass
component: PressButton
widget_type: button
file: runestone/src/components/PressButton.tsx
---

# accessibility/component — PressButton v2

Component: `PressButton`  
Widget type: `button`  
Violations: `0`  
APG keyboard model: `pass`  
Base UI primitive: `used`  
Runtime tests required: `yes`

## Static validation

- Uses the native button semantic through Base UI `ButtonPrimitive`.
- Spreads primitive props via `...props`, preserving the button API including `disabled` and `focusableWhenDisabled`.
- Does not manually strip `disabled` or replace it with `aria-disabled`.
- Includes the required keyboard-focus indicator:
  `focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[var(--pr-focus-ring)]`
- Uses CSS pseudo-classes for interaction state styling and does not introduce `useHover`, `useFocusRing`, `useFocusWithin`, custom `data-hovered`, or custom `data-pressed` state wiring.
- Does not use `asChild`, Slot, or react-aria hooks.

## Notes

- The component is structurally accessible as a button wrapper.
- Accessible naming remains usage-dependent. If a consumer renders an icon-only button, they must supply `aria-label` or `aria-labelledby`.

## Runtime tests required

- Verify `Enter` activates the button.
- Verify `Space` activates the button.
- Verify `disabled` blocks keyboard activation.
- Verify a click or press handler is not invoked when `disabled`.
- Verify `focusableWhenDisabled={true}` keeps the button in the tab order.
- Verify `focusableWhenDisabled={false}` removes the button from the tab order.
- Verify the focus ring appears on keyboard focus and is not shown on mouse click alone.
- Verify focus remains on the button after activation unless the action removes it from the page.

## Final status

Pass on static validation. Runtime behavior still requires explicit tests, especially for disabled-state semantics and `focusableWhenDisabled`.
