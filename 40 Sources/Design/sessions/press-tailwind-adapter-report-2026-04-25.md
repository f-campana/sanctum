# Press Tailwind Adapter Mapping Report

**Date:** 2026-04-25  
**Scope:** Press Rune token mapping to the FODMAPP Tailwind v4 semantic slot contract  
**Status:** Research only. No adapter CSS created.  
**Target:** `sanctum/00 Inbox/` for human review

## Sources Read

- `bifrost/CODEX.md`
- `bifrost/system-spec-v0.3.md`
- `bifrost/AGENTS.md`
- `sanctum/AGENTS.md`
- `bifrost/contracts/design-pipeline-contract.md`
- `sanctum/10 Knowledge/Design/runes/press.md`
- `/Users/fabiencampana/Documents/fodmapp/packages/tailwind-config/src/semantic-slot-map.mjs`
- `/Users/fabiencampana/Documents/fodmapp/packages/tailwind-config/foundation.css`
- `/Users/fabiencampana/Documents/fodmapp/packages/ui/src/components/ui/foundation/button.tsx`
- Supporting FODMAPP usage check:
  `kbd.tsx`, `typography.tsx`, and UI component grep for `font-mono`, `ring`,
  `muted`, `destructive`, and `radius`

## Executive Decision

Press can be adapted onto the FODMAPP Tailwind v4 slot model, but the adapter is
only part of the job.

The token mapping is straightforward for canvas, text, primary action, muted
surface, and fonts. The gaps are semantic, not structural:

- Press has no dedicated radius token even though the Rune requires radius `0`
  everywhere.
- Press has no dedicated focus-ring token even though FODMAPP components use
  `--color-ring` and `--color-ring-soft`.
- Press has no destructive / validation token family even though FODMAPP
  components consume destructive and validation slots.
- Press already has a muted surface token. It does not need a new muted token.

There is one important implementation constraint: a token adapter alone will not
make all FODMAPP components look like Press. Several components still hard-code
non-zero radii, `rounded-full`, 1px borders, or shadows. Those cases need
component-level edits after the adapter exists.

## 1. Press to Tailwind Slot Mapping

Reference point: FODMAPP `semantic-slot-map.mjs` and `foundation.css` define the
actual Tailwind runtime aliases used by components.

| Tailwind slot | FODMAPP semantic intent | Press source token | Decision |
|---|---|---|---|
| `--color-primary` | action primary background | `--pr-orange` | Correct direct mapping. Press uses orange as the only structural/action colour. |
| `--color-background` | page canvas | `--pr-bg` | Correct direct mapping. This is the Press page background token. |
| `--color-foreground` | default text | `--pr-text` | Correct direct mapping. This is the Press primary text token. |
| `--color-border` | default visible border | `--pr-border` | Correct direct mapping. Press borders are structural, dark, and should default to the strongest border token. |
| `--color-muted` | muted / secondary surface | `--pr-surface-mid` | Correct direct mapping. This is the closest Press equivalent to FODMAPP muted surfaces. |
| `--color-muted-foreground` | secondary UI text | `--pr-text-2` | Correct direct mapping. This is the closest Press equivalent to FODMAPP muted text. |
| `--font-sans` | body font family | `--pr-font-body` | Correct direct mapping. FODMAPP maps `font-sans` to its body family. Press body family is DM Sans. |
| `--font-mono` | mono font family | `--pr-font-mono` | Correct visual mapping, but this slot is missing from FODMAPP `foundation.css` today. Add it for Tailwind parity because components already use `font-mono`. |
| `--radius` | control radius | none in current Press tokens | No direct `--pr-*` token exists. Define `--pr-radius-control: 0px` and map `--radius` to it. |
| `--color-ring` | focus border / ring colour | no dedicated token; current visual source is `--pr-orange` | Define `--pr-focus-ring: var(--pr-orange)` and map `--color-ring` to that alias. Do not wire the slot straight to a raw colour without naming the semantic role. |

### Additional mapping notes

- `--font-serif` should map to `--pr-font-display`, because FODMAPP maps
  `font-serif` to its display family and Press headings use Syne.
- `--color-surface` / `--color-card` / `--color-popover` should map to
  `--pr-surface`.
- `--color-surface-muted` should map to `--pr-surface-mid`.
- `--color-surface-inverse` should map to `--pr-surface-dark`.
- `--color-foreground-inverse` should map to `--pr-text-inv`.
- `--color-border-subtle` should map to `--pr-border-light`.
- `--color-border-strong` should map to `--pr-border`.
- `--color-ring-soft` should map to a new alias backed by `--pr-orange-dim`.

## 2. Press Tokens With No Direct Tailwind Slot Equivalent

These Press tokens exist, but they do not map cleanly to a current FODMAPP
semantic slot and should be given explicit semantic names in the adapter layer.

| Press token | Why it does not map directly | Recommended semantic name |
|---|---|---|
| `--pr-orange-dim` | It is a structural orange tint, not a generic muted surface. The closest current use is soft focus indication. | `--pr-focus-ring-soft` |
| `--pr-text-3` | FODMAPP has a primary text slot and a muted text slot, but not a tertiary metadata text slot. | `--pr-foreground-subtle` or `--pr-text-subtle` |
| `--pr-orange` in its structural role | `--color-primary` covers action-primary, but Press orange is broader than button semantics. It is also nav structure, active rail, and section accent. | `--pr-structure` or `--pr-accent-structural` |

These Press tokens do have workable existing semantic equivalents and do not need
new names just to enter Tailwind:

- `--pr-surface-dark` -> inverse surface
- `--pr-text-inv` -> inverse foreground
- `--pr-border-mid` / `--pr-border-light` -> control / subtle border roles
- `--pr-surface-mid` -> muted surface

## 3. Adapter CSS Structure

The adapter should copy the FODMAPP `foundation.css` pattern:

1. Define runtime aliases in `@layer base`.
2. Mirror the same aliases in `@theme inline`.
3. Keep dark selectors present for compatibility, but bind them to the same
   Press values because Press has no dark variant.

Illustrative structure:

```css
@import "tailwindcss";
@custom-variant dark (&:where([data-theme=dark], [data-theme=dark] *));
@import url('https://fonts.googleapis.com/css2?family=Syne:wght@700;800&family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500&family=JetBrains+Mono:wght@400;500&display=swap');

@layer base {
  :root,
  [data-theme="light"],
  [data-theme="dark"] {
    color-scheme: light;

    /* Press source tokens */
    --pr-bg: oklch(97% 0.003 100);
    --pr-surface: oklch(100% 0 0);
    --pr-surface-mid: oklch(94% 0.004 100);
    --pr-surface-dark: oklch(13% 0.005 60);
    --pr-text: oklch(13% 0.005 60);
    --pr-text-2: oklch(38% 0.008 60);
    --pr-text-3: oklch(64% 0.008 60);
    --pr-text-inv: oklch(97% 0.003 100);
    --pr-orange: oklch(57% 0.205 38);
    --pr-orange-dim: oklch(57% 0.205 38 / 0.08);
    --pr-border: oklch(13% 0.005 60);
    --pr-border-mid: oklch(80% 0.006 100);
    --pr-border-light: oklch(88% 0.005 100);
    --pr-font-display: "Syne", sans-serif;
    --pr-font-body: "DM Sans", sans-serif;
    --pr-font-mono: "JetBrains Mono", monospace;

    /* New semantic aliases required for Tailwind parity */
    --pr-radius-control: 0px;
    --pr-focus-ring: var(--pr-orange);
    --pr-focus-ring-soft: var(--pr-orange-dim);

    /* Tailwind runtime aliases */
    --color-background: var(--pr-bg);
    --color-foreground: var(--pr-text);
    --color-surface: var(--pr-surface);
    --color-surface-muted: var(--pr-surface-mid);
    --color-surface-inverse: var(--pr-surface-dark);
    --color-foreground-inverse: var(--pr-text-inv);
    --color-card: var(--pr-surface);
    --color-card-foreground: var(--pr-text);
    --color-popover: var(--pr-surface);
    --color-popover-foreground: var(--pr-text);
    --color-muted: var(--pr-surface-mid);
    --color-muted-foreground: var(--pr-text-2);
    --color-border: var(--pr-border);
    --color-border-subtle: var(--pr-border-light);
    --color-primary: var(--pr-orange);
    --color-primary-foreground: var(--pr-text-inv);
    --color-ring: var(--pr-focus-ring);
    --color-ring-soft: var(--pr-focus-ring-soft);
    --font-sans: var(--pr-font-body);
    --font-serif: var(--pr-font-display);
    --font-mono: var(--pr-font-mono);
    --radius: var(--pr-radius-control);
  }
}

@theme inline {
  --color-background: var(--pr-bg);
  --color-foreground: var(--pr-text);
  --color-surface: var(--pr-surface);
  --color-surface-muted: var(--pr-surface-mid);
  --color-surface-inverse: var(--pr-surface-dark);
  --color-foreground-inverse: var(--pr-text-inv);
  --color-card: var(--pr-surface);
  --color-card-foreground: var(--pr-text);
  --color-popover: var(--pr-surface);
  --color-popover-foreground: var(--pr-text);
  --color-muted: var(--pr-surface-mid);
  --color-muted-foreground: var(--pr-text-2);
  --color-border: var(--pr-border);
  --color-border-subtle: var(--pr-border-light);
  --color-primary: var(--pr-orange);
  --color-primary-foreground: var(--pr-text-inv);
  --color-ring: var(--pr-focus-ring);
  --color-ring-soft: var(--pr-focus-ring-soft);
  --font-sans: var(--pr-font-body);
  --font-serif: var(--pr-font-display);
  --font-mono: var(--pr-font-mono);
  --radius: var(--pr-radius-control);
}
```

### Dark mode strategy

Press should be explicit, not ambiguous:

- Keep the `dark` variant selector only for host-app compatibility.
- Bind `[data-theme="dark"]` to the same values as `:root` and
  `[data-theme="light"]`.
- Set `color-scheme: light`.
- Do not define a second token branch.
- If a product truly needs dark mode, that is not a Press adapter tweak. It is a
  Rune version review or a different Rune.

## 4. New Semantic Aliases Press Still Needs

### Required

| Needed alias | Why it is needed | Initial mapping |
|---|---|---|
| `--pr-radius-control` | FODMAPP exposes `--radius`, but Press only states a rule, not a token. | `0px` |
| `--pr-focus-ring` | FODMAPP focus styling uses a named ring slot. Press currently only describes focus by rule. | `var(--pr-orange)` |
| `--pr-focus-ring-soft` | FODMAPP components use a second soft ring layer. | `var(--pr-orange-dim)` |
| `--pr-destructive` family | Buttons, badges, alerts, and validation states already consume destructive slots. | New minimal-footprint red family |
| `--pr-validation-error` family | Inputs and fields consume validation border, ring, and text slots. | New minimal-footprint error family |

### Recommended

| Recommended alias | Why it helps |
|---|---|
| `--pr-structure` | Preserves the Press rule that orange is structural, not just action-primary. |
| `--pr-foreground-subtle` | Gives `--pr-text-3` a semantic home instead of leaving it as an orphan token. |

### Not needed

| Example | Decision |
|---|---|
| muted surface alias | Not needed. `--pr-surface-mid` already fills this role cleanly. |
| body / display / mono aliases | Not needed. `--pr-font-body`, `--pr-font-display`, and `--pr-font-mono` already exist. |

## 5. Implementation Constraint Beyond Tokens

The adapter will not by itself enforce the full Press Rune.

Observed FODMAPP component constraints:

- `button.tsx` uses `border`, not `border-2`, so Press's 2px border rule is not
  satisfied by token mapping alone.
- `kbd.tsx` and multiple other components still use shadows, while Press forbids
  shadows except focus indication.
- Several components use fixed `rounded-full`, `rounded-md`, or
  `rounded-[min(var(--radius-sm),8px)]`, so Press's zero-radius rule is not
  satisfiable by `--radius: 0` alone.

Conclusion:

- The adapter CSS is necessary.
- A follow-up component audit is also necessary if the goal is true Press
  compliance rather than approximate colour/type theming.

## Recommended Next Step

Create the adapter CSS only after human review of this report, with these
decisions locked first:

1. Approve the core slot mapping table above.
2. Approve the new semantic alias names for radius, focus ring, and destructive /
   validation states.
3. Decide whether `--pr-structure` and `--pr-foreground-subtle` should be added
   now or deferred.
4. Plan a second pass for component-level Press compliance: 2px borders, no
   shadows, and zero-radius hard overrides.
