---
type: run-report
skill: accessibility/component
date: 2026-05-01
status: pass
component: PressButtonLink
widget_type: link
file: runestone/src/components/PressButtonLink.tsx
---

# accessibility/component — PressButtonLink

Component: `PressButtonLink`
Widget type: `link`
Violations: `0`
APG keyboard model: `pass`
Base UI primitive: `not-applicable`
Runtime tests required: `no`

## Static validation

- Uses a native `<a>` element for link semantics.
- Does not assign an ARIA role or reimplement link semantics on a
  non-interactive element.
- Preserves native anchor props by extending `React.ComponentProps<'a'>`
  and spreading `...props` onto the `<a>`.
- Does not import or use a Base UI primitive. This is correct for
  `PressButtonLink` because Base UI has no Anchor primitive and the ADR
  directs native HTML use when no Base UI primitive exists.
- Does not use Radix Slot, `asChild`, react-aria hooks, manual keyboard
  handlers, custom focus state, custom press state, `aria-disabled`, or
  disabled-state manipulation.
- Includes the shared Press focus-visible outline classes through
  `pressButtonVariants`.

## Notes

- Native anchors handle focus, `Enter` activation, and link semantics
  without an ARIA wrapper.
- Accessible naming remains usage-dependent. If a consumer renders only
  non-text content, they must provide an accessible name.
- A valid navigation target remains usage-dependent. Consumers should pass
  `href` for navigation links.

## Runtime tests required

No component-level runtime tests are required by this wrapper. It adds no
custom keyboard, click, disabled, or focus-management behavior beyond the
native anchor element.

## Final status

Pass on static accessibility validation for `widget_type: link`.
