---
type: session-summary
date: 2026-04-26
thread: claude
project: sanctum-bifrost
status: ready-for-ingest
---

# Session Summary — Component Architecture Pivot and PressButton v2

**Date:** 2026-04-25 → 2026-04-26
**Thread:** Claude (this conversation)
**Duration:** Extended session (~12 hours)
**Target location:** `sanctum/40 Sources/Design/sessions/component-architecture-pivot-2026-04-26.md`

---

## What this session was

A deliberate architectural correction triggered by the PressButton v1
code review. The session started with three independent reviews of
PressButton v1 — 208 lines using react-aria hooks, Radix Slot, and
manual mergeProps — that identified the same structural issues. Rather
than patching v1, the session used the evidence as the basis for a
complete architectural review of the component library approach.

The session produced: a component architecture ADR grounded in direct
source code inspection, updated skills for react/component and
accessibility/component, the PressButton v2 rewrite (58 lines, zero
violations), and the PressGallery component with live state simulation.

It also caught and fixed three systemic infrastructure issues: the
Tailwind utility cascade being broken by the press.css global reset,
the @import ordering warning in press-tailwind.css, and the
renderToStaticMarkup bypass of Astro's scoped style system.

---

## Decisions made — confirmed and locked

**Base UI replaces React Aria hooks as the behavioral primitive layer.**
Direct inspection of four source files — Adobe React Spectrum Button,
Base UI Button, shadcn/ui Radix Button, shadcn/ui Base UI Button —
produced the evidence. Base UI's ButtonPrimitive absorbs all mergeProps,
ref management, ARIA forwarding, and data-* exposure internally. The
consumer component becomes 5 lines wrapping CVA. React Aria Components
was discussed in research but not inspected — it is not cited as direct
evidence in the ADR.

**No asChild. PressButton + PressButtonLink as separate components.**
Adobe's production Button + LinkButton split is the strongest evidence.
Both P1 bugs in PressButton v1 lived in the asChild path. The pattern
forces element type detection at runtime and creates type collisions.
Separate components share CVA variant definitions.

**CSS pseudo-classes for interaction states on simple components.**
`hover:`, `focus-visible:`, `disabled:`, `active:`, `aria-invalid:`
replace useHover, useFocusRing, and manual data-* spreading. The
shadcn/ui 2025 source confirmed this direction. Simple primitives
do not need JS state machines.

**`focusableWhenDisabled` via Base UI prop, not manual aria-disabled.**
Base UI exposes this as a first-class prop. Manual disabled attribute
stripping — the P1 pattern from v1 — is no longer needed or permitted.

**`cn()` = clsx + tailwind-merge required for all class composition.**
Concatenation without merge produces non-deterministic Tailwind class
resolution. The override boundary is documented: overrides that
violate Press inviolable rules are unsupported.

**React 19 idioms throughout: no forwardRef.**
Hydration boundary is context-dependent: in Astro, `client:*` on the
page; in RSC frameworks, `'use client'` in the component file. The
component library is agnostic about which context it runs in.

**System tokens for destructive/validation states outside --pr- namespace.**
`--sys-error`, `--sys-success`, `--sys-warning` sit outside the Rune
identity. Press inviolable Rule 5 remains clean.

**Component distribution follows the owned source model.**
Components are copied into consuming projects, not installed as a
versioned package. Legibility for agents is a first-class constraint.

**press.css global reset must be inside @layer base.**
The universal `* { padding: 0; margin: 0; }` reset must be wrapped in
`@layer base` so Tailwind utilities in `@layer utilities` override it.
Without this, all padding and margin utilities are silently overridden.
Anti-pattern added to press.md section 10.

---

## Artifacts produced

### ADR and skill updates

| Artifact | Target path | Status |
|---|---|---|
| Component architecture ADR | `sanctum/10 Knowledge/Concepts/press-component-architecture-adr.md` | committed |
| react/component skill v1.1 | `bifrost/skills/react/react-component/SKILL.md` | committed |
| accessibility/component skill v1.1 | `bifrost/skills/accessibility/accessibility-component/SKILL.md` | committed |

### Component library

| Artifact | Target path | Status |
|---|---|---|
| PressButton v2 | `runestone/src/components/PressButton.tsx` | committed |
| PressGallery | `runestone/src/components/PressGallery.astro` | committed |
| cn() utility | `runestone/src/lib/utils.ts` | committed |

### Infrastructure

| Artifact | Target path | Status |
|---|---|---|
| press.css @layer base fix | `runestone/public/styles/press.css` | committed |
| press-tailwind.css @import order fix | `runestone/src/styles/press-tailwind.css` | committed |
| Base UI installed | `runestone/package.json` | committed |
| tailwind-merge + clsx installed | `runestone/package.json` | committed |
| Playwright installed | `runestone/package.json` | committed |
| @astrojs/react installed | `runestone/package.json` | committed |
| CODEX.md component primitive rule | `bifrost/CODEX.md` | committed |
| frontend/component skill CSS layer note | `bifrost/skills/frontend/frontend-component/SKILL.md` | committed |

### Source material promoted

| Artifact | Target path | Status |
|---|---|---|
| Gallery diagnostic report | `sanctum/40 Sources/Design/sessions/gallery-diagnostic-2026-04-26.md` | committed |
| PressButton v1 run reports (3, superseded) | `sanctum/40 Sources/Design/sessions/` | committed |
| PressButton v2 run reports (3) | `sanctum/40 Sources/Design/sessions/` | committed |
| PressGallery run report | `sanctum/40 Sources/Design/sessions/` | committed |

---

## What was validated

**PressButton v2 passed all three skill validations on first dispatch.**
react/component: pass. typescript/component: pass (corrected tsconfig
flags). accessibility/component: pass. Three independent code reviews
confirmed the architecture was correct — 58 lines, Base UI primitive,
CVA variants, CSS pseudo-classes, zero hooks.

**The Playwright diagnostic correctly identified the cascade bug.**
`px-5` and `py-2.5` were present in the class attribute and in the
built CSS but computed padding was `0px`. The global reset in press.css
outside any layer was winning over Tailwind utilities in `@layer utilities`.
The fix: wrap the reset in `@layer base`.

**The renderToStaticMarkup approach bypassed Astro's scoped CSS.**
PressGallery originally used `renderToStaticMarkup` + `set:html` to
inject buttons. Scoped CSS rules with `:global()` could not reach them
because the injected HTML bypassed Astro's component tree. The fix:
render PressButton directly in the Astro template. This also required
installing `@astrojs/react` as a Vite integration.

**All five button states now display without user interaction.**
PressGallery shows DEFAULT, HOVER, ACTIVE, DISABLED, and FOCUS for
both primary and ghost variants via CSS-forced state simulation scoped
to the gallery component. PressButton is unchanged.

---

## Systemic lessons — encoded in skills and CODEX

**The cascade issue will recur without the @layer fix.**
Any project using press.css with Tailwind must wrap the global reset
in `@layer base`. This is now in press.md section 10 anti-patterns and
in the frontend/component skill.

**renderToStaticMarkup + set:html bypasses Astro scoped CSS.**
Any Astro component that injects React components via set:html will
lose scoped style targeting. Render React components directly in the
Astro template.

**Agent-produced component complexity scales with spec complexity.**
PressButton v1 was 208 lines because the spec said "use React Aria
hooks, Radix Slot, CVA." PressButton v2 is 58 lines because the spec
said "use Base UI ButtonPrimitive, CVA, CSS pseudo-classes." The spec
is the template. Simpler specs produce simpler, more correct output.

---

## Open items — not blocking current phase

- **PressButtonLink**: the companion component. Trivial given the ADR
  and template. Not yet built.
- **/runes/press/spec route**: the markdown content dump currently sits
  at the bottom of the main experience page. Should move to a separate
  route so the main page is pure experience.
- **Runestone 4 commits ahead of origin**: local commits not yet pushed.
- **Pending descriptions in index.md**: all rows still have
  `[pending description]`. Human task, quiet pass.
- **PressButton v1 PressButton.tsx**: was committed to runestone during
  v1 session, then deleted before v2. Confirmed absent from working tree.
- **Runtime tests for PressButton**: the accessibility/component skill
  requires tests for disabled state suppression, focusableWhenDisabled
  tab-stop behaviour, and keyboard-only focus ring. Not yet written.

---

## Things to not repeat

- Do not specify react-aria hooks in a component spec — the correct
  primitive layer is Base UI.
- Do not use renderToStaticMarkup + set:html for React components in
  Astro — render them directly.
- Do not place global CSS resets outside @layer — wrap in @layer base.
- Do not put @import url() after @import "tailwindcss" when using
  PostCSS — PostCSS expands the local import first, breaking CSS spec.
- Do not produce a component gallery with all buttons in resting state —
  each state tile must show its state without user interaction.

*Session summary ready for ingest into Sanctum/40 Sources/Design/sessions/*
