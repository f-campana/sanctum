---
type: concept-note
status: active
updated: 2026-04-25
tags: [react, components, architecture, press, adr, decisions]
---

# ADR — Press Component Library Architecture

Architectural decisions for the Press component library. Grounded in
direct inspection of Base UI, React Aria Components, shadcn/ui (Radix
version), and shadcn/ui (Base UI version) source code, plus review of
the first PressButton implementation produced by the pipeline.

Update this document when decisions change. Cite the evidence that
changed them. Skills reference this document — drift here propagates
to every component the pipeline produces.

---

## Context

The Press component library is produced by AI agents (Claude Code,
Codex) dispatched through a skill pipeline. This creates a constraint
that does not exist in typical component library design: the template
an agent uses must be simple enough to produce correctly at scale, and
legible enough that a future agent can read and modify it without
misunderstanding what it does.

The PressButton v1 was substantially larger than equivalent
implementations in the libraries we studied, and exposed the cost of
combining low-level hooks, Slot-based polymorphism, and manual prop
merging. Three independent code reviews identified the same structural
issues. The complexity was not a style problem — it was an abstraction
level problem.

The architecture decisions below are constrained by this context.

---

## Evidence base

Four source files were read directly and constitute the evidence base
for these decisions. React Aria Components was discussed in broader
research but its source was not read directly — it is not cited as
direct evidence here.

**Adobe React Spectrum Button** — production design system at scale.
~300 lines. Uses two separate components: `Button` (renders `<button>`)
and `LinkButton` (renders `<a>`). No asChild. No polymorphism via Slot.
The most mature implementation in the set made the explicit decision to
split rather than polymorph.

**Base UI Button** — `@base-ui/react`. ~55 lines. Uses
`useButton` and `useRenderElement` internally, exposing
`focusableWhenDisabled` and `nativeButton` as first-class props. All
mergeProps, ref merging, and data-* conversion absorbed internally. The
consumer sees a clean five-prop API.

**shadcn/ui Button (Radix version)** — current 2025 source. ~15 lines.
`Slot.Root` for asChild, CVA for variants, CSS pseudo-classes for all
interaction states. No hooks. `hover:`, `focus-visible:`, `disabled:`,
`aria-invalid:` handle what our v1 implemented with three React Aria
hooks.

**shadcn/ui Button (Base UI version)** — current 2025 source. ~5 lines.
`ButtonPrimitive` from Base UI, CVA for variants, `cn()` for class
merging. No asChild. `ButtonPrimitive.Props` spread gives
`focusableWhenDisabled` without any manual wiring.

---

## Decisions

### D1 — No asChild. Explicit components per element type.

`PressButton` renders a `<button>`. `PressButtonLink` renders an `<a>`.
These are separate components sharing the same CVA variant definitions.

**Evidence:** Adobe's Button + LinkButton split is the strongest signal.
The most mature implementation in the set, with the most resources to
implement asChild correctly, chose not to. Both P1 bugs in PressButton
v1 lived in the asChild path. The asChild pattern forces element type
detection at runtime, creates type collisions, and adds a dependency
that is otherwise not needed.

**Consequence:** When a consumer needs a link that looks like a button,
they use `PressButtonLink`, not `PressButton asChild`. Two component
names is less elegant. It is more correct and more legible.

---

### D2 — Base UI is the default behavioral primitive layer.

All interactive components use `@base-ui/react` as the
behavioral primitive unless a specific exception is recorded in this
ADR. Not react-aria hooks. Not react-aria-components. Not Radix UI
primitives.

**Evidence:** The Base UI shadcn/ui button wrapper is five lines with
no accessibility wiring required from the consumer. `focusableWhenDisabled`
is a first-class prop. `nativeButton` solves the element type problem
that caused PressButton's P1 bugs. Base UI is actively maintained;
Radix is in maintenance mode.

**What Base UI handles:** keyboard activation, focus management, ARIA
roles and attributes, press event normalization across mouse/touch/
keyboard, `focusableWhenDisabled`, `data-*` state exposure for complex
composites.

**What we handle:** visual presentation, Press token application, CVA
variant definitions, Tailwind class composition.

**Exceptions:** react-aria hooks may be used when no Base UI primitive
covers the use case. Any exception must be documented here with the
specific reason. The exception does not become a default.
When no Base UI primitive exists, use the native HTML element directly. Document the gap in the run report and check for a Base UI update before building the next version of the component. PressButtonLink is the first application of this exception — it renders a native <a> because @base-ui/react has no Anchor primitive at v1.4.1.

---

### D3 — CSS pseudo-classes for interaction states on simple components.

Simple components (Button, Badge, Tag, Input) style interaction states
via Tailwind CSS pseudo-class modifiers: `hover:`, `focus-visible:`,
`disabled:`, `active:`, `aria-invalid:`, `aria-expanded:`,
`aria-selected:`. JavaScript does not set these states.

**Evidence:** The shadcn/ui Radix button (2025 source) uses zero
JavaScript state machines for interaction styling. This is simpler,
more legible, SSR-safe, and produces no hydration mismatches.

**When JS-driven data-* is appropriate:** complex composites where CSS
pseudo-classes are insufficient — e.g. a listbox that needs
`data-selected` to style sibling elements. Base UI exposes these
automatically for composites that need them. Simple primitives do not
need JS state machines.

**The line:** if the state is expressible as a native CSS pseudo-class
or ARIA attribute Tailwind can target, use CSS. Otherwise use Base UI's
built-in data-* exposure — do not add custom hooks.

---

### D4 — Disabled state via `focusableWhenDisabled`, not manual wiring.

When a disabled interactive element should remain in the tab order,
pass `focusableWhenDisabled` to the Base UI primitive. Do not manually
strip the native `disabled` attribute and replace it with `aria-disabled`.

**Default:** `focusableWhenDisabled={false}` — disabled elements are
removed from the tab order. Set to `true` explicitly when the component
needs to be discoverable while disabled (typically when a tooltip
explains why).

**On disabled press suppression:** Base UI suppresses press events
when `disabled` is true, regardless of `focusableWhenDisabled`. If a
component adds custom DOM click handlers, those handlers must not bypass
disabled semantics — Base UI does not suppress native DOM `click` events
on non-button elements.

**Runtime test requirement:** disabled state semantics cannot be
verified by static skill validation. Every interactive component must
include tests covering: keyboard activation blocked when disabled,
click handler not invoked when disabled, focus ring not shown on mouse
click. Static analysis is necessary but not sufficient.

---

### D5 — CVA for all variant management.

All components use `class-variance-authority` for variant definitions.
No variant logic in component props or conditionals.

**The CVA base string encodes Press inviolable rules structurally:**
```
"border-2 border-solid rounded-none shadow-none"
```
This string must appear in the base of every Press component. An agent
producing a new component copies this string. The inviolable rules are
inherited from the template, not recalled from the skill file.

**No size variants until a second size exists.** A size prop with one
value is indirection with no benefit.

---

### D6 — `cn()` = clsx + tailwind-merge for class composition.

All components use `cn()` for merging CVA output with consumer-supplied
`className`. Concatenation without merge produces non-deterministic
Tailwind class resolution.

```typescript
import { clsx, type ClassValue } from 'clsx'
import { twMerge } from 'tailwind-merge'

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs))
}
```

**The override boundary:** `cn()` allows consumers to override any
utility class, including Press inviolable rules. Overrides that violate
Press inviolable rules (`rounded-none`, `border-2`, `shadow-none`) are
unsupported. The function does not enforce this — the documentation does.

---

### D7 — React 19 idioms. Hydration boundary is context-dependent.

**React 19:**
- No `forwardRef` — ref is a regular prop.
- Do not add `useMemo` or `useCallback` manually. The React Compiler
  handles memoization. Manual memoization is technical debt.
- `VariantProps<typeof variantFn>` drives prop types — do not hand-mirror
  variant unions in the interface.

**Hydration boundary — context-dependent, not universal:**
- In Astro (current system): hydration is controlled at the page level
  via `client:*` directives on the `.astro` file. Do not add `'use client'`
  inside component files — it is not the Astro convention and has no
  effect in this context.
- In RSC frameworks (Next.js App Router): interactive components require
  `'use client'` at the top of the file. Add it when the component is
  consumed in an RSC context.

The Press component library should remain agnostic about the hydration
boundary. The consuming framework determines where the boundary sits.

---

### D8 — System tokens for destructive and validation states.

These tokens are outside the Rune namespace and must be treated as
system utilities, not Press identity tokens. Press inviolable Rule 5
permits "semantic colours beyond success/error states at minimum
footprint."

```css
--sys-error:          oklch(55% 0.22 25);
--sys-error-dim:      oklch(55% 0.22 25 / 0.1);
--sys-success:        oklch(55% 0.16 145);
--sys-success-dim:    oklch(55% 0.16 145 / 0.1);
--sys-warning:        oklch(70% 0.18 85);
--sys-warning-dim:    oklch(70% 0.18 85 / 0.1);
```

These map to Tailwind as:
- `--color-destructive` → `var(--sys-error)`
- `--color-destructive-foreground` → `var(--pr-text-inv)`

The Press Rune stays clean. Components that need validation states use
system tokens. Components that do not need them do not reference them.
Introducing system tokens into `--pr-*` namespace is a violation of
Rule 5.

---

### D9 — Component distribution follows the owned source model.

Components are owned source code, not versioned dependencies. When a
component is added to the Press library, it is copied into the consuming
project. The consuming project owns and can modify it.

This is why the component template must be simple: a consumer who needs
to modify a 200-line component with multiple library integrations is
unlikely to do so correctly. A consumer who needs to modify a 30-line
component with CVA variants and a Base UI primitive will.

This is the same model as shadcn/ui — not a dependency on shadcn/ui
itself, but the same distribution principle: source you own, not a
black box you depend on.

---

## Component template

Every Press component follows this structure:

```typescript
// In RSC frameworks: add 'use client' here.
// In Astro: hydration is handled by client:* on the page, not here.

import { [Primitive] as [Primitive]Primitive } from '@base-ui/react/[primitive]'
import { cva, type VariantProps } from 'class-variance-authority'
import { cn } from '@/lib/utils'

const press[Component]Variants = cva(
  [
    // Press inviolable rules — never remove these three
    'border-2 border-solid rounded-none shadow-none',
    // Base styles
    '...',
    // Focus — keyboard only, Press token
    'focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2',
    'focus-visible:outline-[var(--pr-focus-ring)]',
  ],
  {
    variants: {
      variant: {
        primary: [...],
        ghost: [...],
      },
    },
    defaultVariants: { variant: 'primary' },
  }
)

export interface Press[Component]Props
  extends [Primitive]Primitive.Props,
    VariantProps<typeof press[Component]Variants> {}

export function Press[Component]({
  className,
  variant,
  ...props
}: Press[Component]Props) {
  return (
    <[Primitive]Primitive
      className={cn(press[Component]Variants({ variant, className }))}
      {...props}
    />
  )
}
```

---

## What changed from PressButton v1

| v1 | This ADR |
|---|---|
| react-aria useButton + useHover + useFocusRing | Base UI ButtonPrimitive |
| Radix Slot for asChild | No asChild — PressButton + PressButtonLink |
| Manual mergeProps + data-* spreading | CSS pseudo-classes |
| Manual aria-disabled stripping | focusableWhenDisabled prop |
| P1: onClick still fires when disabled | Base UI suppresses press; custom click handlers must preserve semantics |
| `'use client'` missing | Hydration boundary is context-dependent |
| forwardRef wrapper | ref as regular prop (React 19) |

---

## What this does not decide

- Whether to use Storybook or an equivalent for component documentation.
- Testing framework or tooling — only that tests are required for
  disabled semantics on interactive components.
- Packaging and distribution format for consuming projects.
- Whether Base UI covers every future primitive need. If it does not,
  update this ADR before reaching for another library.
