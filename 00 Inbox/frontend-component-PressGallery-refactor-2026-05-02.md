# frontend-component-PressGallery-refactor-2026-05-02

## dispatch summary

Refactor `runestone/src/components/PressGallery.astro` into the single source for the Press spec gallery copy, remove the duplicate inlined gallery from `runestone/src/pages/runes/press/spec.astro`, verify `/runes/press/spec` still renders the expected Press gallery and supporting prose, write this Inbox run report, run `wiki/index-rebuild`, and produce separate `runestone` and `sanctum` commits.

## actions taken

- `runestone/src/components/PressGallery.astro` — `8 added, 20 removed`
  Verbatim added text:
  ```md
  CSS-simulated hover treatment for implementation reference.
  CSS-simulated press state for implementation reference.
  CSS-simulated focus ring for implementation reference.
  All ten Press button states rendered live across both PRIMARY and GHOST variants.
  Reference when implementing Press buttons in product surfaces.
  All states CSS-simulated via data attributes · no JavaScript · no interaction required.
  ```
  Removed obsolete copy-only styling:
  - `.press-gallery__intro code`
  Props interface review:
  - Confirmed unchanged. `PressGallery.astro` had no exported `Props` interface before this dispatch and still has none after it.

- `runestone/src/pages/runes/press/spec.astro` — `1 added, 299 removed`
  Self-edit removal: `runestone/src/pages/runes/press/spec.astro` — removed inlined Press gallery markup and scoped dead selectors — reason single-source collapse back into `PressGallery`.
  Actions:
  - Replaced the duplicated gallery frontmatter, markup, and gallery-specific scoped CSS with a single `<PressGallery />` invocation.
  - Added `import PressGallery from '../../../components/PressGallery.astro';`.
  - Removed the duplicated `PressButton` import and all route-local gallery state definitions.
  Removed dead selectors:
  - `.press-gallery`
  - `.press-gallery__inner`
  - `.press-gallery__header`
  - `.press-gallery__title`
  - `.press-gallery__count`
  - `.press-gallery__intro`
  - `.press-gallery__focus-note`
  - `.press-gallery__focus-note-rule, .press-gallery__eyebrow-rule`
  - `.press-gallery__columns`
  - `.press-gallery__column`
  - `.press-gallery__eyebrow`
  - `.press-gallery__states`
  - `.press-gallery__state`
  - `.press-gallery__state--full-width`
  - `.press-gallery__button-frame`
  - `.press-gallery__button-frame :global(button)`
  - `.press-gallery__column[aria-labelledby='press-gallery-primary'] [data-state='hover'] :global(.press-gallery__button-frame button:not([disabled]))`
  - `.press-gallery__column[aria-labelledby='press-gallery-ghost'] [data-state='hover'] :global(.press-gallery__button-frame button:not([disabled]))`
  - `[data-state='active'] :global(.press-gallery__button-frame button:not([disabled]))`
  - `[data-state='focus'] :global(.press-gallery__button-frame button)`
  - `.press-gallery__state-label`
  - `.press-gallery__state-note`
  - `@media (max-width: 900px) .press-gallery__columns`
  - `@media (max-width: 720px) .press-gallery__header`
  - `@media (max-width: 720px) .press-gallery__column`
  - `@media (max-width: 720px) .press-gallery__states`
  - `@media (max-width: 720px) .press-gallery__state--full-width`

- `sanctum/00 Inbox/frontend-component-PressGallery-refactor-2026-05-02.md` — `added`
  This run report records the component refactor, verification commands, selector removals, and commit SHAs produced by the session.

## verification commands run with output

```text
$ curl -s -o /dev/null -w '%{http_code}\n' http://127.0.0.1:4321/runes/press/spec
200
```

```text
$ curl -s -o /dev/null -w '%{http_code}\n' http://127.0.0.1:4321/runes/press
200
```

```text
$ curl -s -o /dev/null -w '%{http_code}\n' http://127.0.0.1:4321/
200
```

```text
$ grep -nE 'data-state="(default|hover|active|disabled|focus)"' runestone/src/pages/runes/press/spec.astro
```

## deviations from the brief, if any

None.

## commit SHAs produced

- `runestone` — `ae6478eec6cd5be2da05f7a08f2bb0661e231f69`
- `sanctum` — pending
