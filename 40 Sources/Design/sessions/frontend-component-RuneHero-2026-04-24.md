# frontend/component - RuneHero

Date: 2026-04-24
Design Contract: `runestone/DESIGN_RUNESTONE.md`
Component: `runestone/src/components/RuneHero.astro`

## Dispatch

Build a static Astro `RuneHero` component for the top identity section of a Rune page.

## Props

- `name: string`
- `status: string`
- `archetypes: string[]`
- `version: string`
- `namespace: string`
- `test_sentence: string`

## Output

Component: RuneHero
Lines: 155

## Press Inviolable Rule Checks

- Rule 1 - Orange is structural, never decorative: pass. Orange is used only for the horizontal rule element before the eyebrow text.
- Rule 2 - Zero radius, everywhere: pass. The component declares no `border-radius`; the global reset owns radius.
- Rule 3 - 2px borders throughout: pass. All visible borders and separators are `2px solid`.
- Rule 4 - Light-first, always: pass. The component uses `var(--pr-surface-bg)` and `var(--pr-surface)` only; no dark hero section or dark-mode variant.
- Rule 5 - One structural colour: pass. The component uses only `var(--pr-orange)` plus neutral `--pr-*` text, surface, and border tokens.

## Notes

- The headline uses `font-size: clamp(32px, 4vw, 64px)` and an overflow-hidden title frame to satisfy the Design Contract display-text anti-pattern fix.
- No page files were modified.
