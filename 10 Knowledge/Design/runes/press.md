---
name: Press
slug: press
version: 1.0.0
status: stable
archetypes: [Creator, Outlaw]
namespace: pr
radar: "6-4-8-8-9-2-4-7"
test_sentence: "Does this look like it was printed by someone who knows exactly what they're doing?"
instances: 1
first_instanced: 2026-04-22
---

# Press

## 01 — Essence

Typography as physical object. The printing press as the founding metaphor — type
pressed into surface, bold and direct, no negotiation. Every border is 2px because
1px is invisible and timid. Every radius is 0 because rounding says "I want to be
liked." The orange nav band is not an accent — it is load-bearing structure, the
first thing you see and the thing that tells you where you are.

Press is for tools that have something to say and say it plainly. Not aggressive —
precise. Not cold — disciplined. The identity recedes exactly as much as necessary
and no further.

The test sentence: "Does this look like it was printed by someone who knows exactly
what they're doing?" If yes, continue. If it looks like a SaaS landing page, a
dark dashboard, or anything that could be mistaken for a Vercel-adjacent product,
recommence.

## 02 — Archetypes

**Creator** (primary) — the craft is visible and intentional. Every spatial
decision — the 2px border weight, the zero radius, the orange as structure not
decoration — is legible as a choice. The person using this tool should sense that
it was made by someone who cares about making things. Not as warmth but as
precision. The care shows in the details, not in the friendliness.

**Outlaw** (secondary) — refusal of the generic. Press exists in opposition to
the rounded-corner, soft-shadow, Inter-on-white aesthetic that dominates SaaS
tooling. This refusal is not decorative — it is load-bearing. Every decision in
this rune is a decision not to default. The orange nav band is the clearest
expression: a structural element that announces itself rather than apologising
for existing.

## 03 — Radar

```
Density      6  — Purposeful — space is earned, not assumed. Components fill their
                  container without cramping. No generous padding for its own sake.
Temperature  4  — Controlled neutral — neither warm nor cold. The orange provides
                  energy without warmth. Off-white base is paper, not skin.
Luminosity   8  — Light-first — white base, dark type, orange structure. No dark
                  mode variant in this rune. Contrast is maximum, always.
Energy       8  — Kinetic — hard press animations, snap transitions, no spring
                  physics. Motion feels mechanical, not organic.
Geometry     9  — Fully geometric — border-radius: 0 everywhere without exception.
                  Grid is visible and rigid. Asymmetry is permitted; softness is not.
Chromatism   2  — Near-monochrome — one structural colour (orange). Black, white,
                  and off-white carry everything else. No secondary accent.
Depth        4  — Restrained — no box-shadows. Depth is created by border weight
                  and background contrast alone. 2px borders at 0 radius read as
                  physical objects stacked on a surface.
Posture      7  — Assertive — the interface has a point of view. It does not recede
                  behind content. It frames it with authority.
```

## 04 — Inviolable Rules

If any one of these conditions fails, the output is not Press. Check each before
delivering.

**Rule 1 — Orange is structural, never decorative.**
```
Is orange (#E84E08 / oklch(57% 0.205 38)) used exclusively as a load-bearing
structural element — nav background, active state background, primary CTA fill,
section accent border — and never as a text highlight, badge background, or
decorative flourish?
  Yes → proceed
  No  → STOP. Orange in this rune is architecture. Remove every decorative use.
```

**Rule 2 — Zero radius, everywhere.**
```
Is border-radius: 0 applied to every element — buttons, cards, badges, inputs,
modals, tags, tooltips?
  Yes → proceed
  No  → STOP. No rounded corners exist in Press. Fix before continuing.
```

**Rule 3 — 2px borders throughout.**
```
Are all visible borders exactly 2px solid? No 1px borders, no 0.5px borders,
no hairlines?
  Yes → proceed
  No  → STOP. 1px borders are invisible against this rune's intention. Fix.
```

**Rule 4 — Light-first, always.**
```
Is the primary page background off-white (#F7F7F5 / oklch(97% 0.003 100))?
Is there no dark-mode variant or dark-background hero section?
  Yes → proceed
  No  → STOP. Press is light-first without exception. Dark sections break the
        rune's identity entirely. Remove them.
```

**Rule 5 — One structural colour.**
```
Does the entire composition use exactly one non-neutral colour (orange #E84E08)?
No secondary accent, no tertiary highlight, no semantic colours beyond
success/error states (which use standard system greens/reds at minimum footprint)?
  Yes → proceed
  No  → STOP. Additional colours dilute the structural authority of the orange.
        Remove all non-orange, non-neutral colour decisions.
```

## 05 — Canvas

All tokens use the `--pr-` namespace prefix.

```css
:root {
  /* Surfaces */
  --pr-bg:            oklch(97% 0.003 100);  /* #F7F7F5 — page background */
  --pr-surface:       oklch(100% 0 0);       /* #FFFFFF — cards, elevated */
  --pr-surface-mid:   oklch(94% 0.004 100);  /* #EFEFEC — section backgrounds */
  --pr-surface-dark:  oklch(13% 0.005 60);   /* #1A1814 — nav on orange, inverted */

  /* Text */
  --pr-text:          oklch(13% 0.005 60);   /* #1A1814 — primary text */
  --pr-text-2:        oklch(38% 0.008 60);   /* #5A5450 — secondary text */
  --pr-text-3:        oklch(64% 0.008 60);   /* #A09890 — tertiary, metadata */
  --pr-text-inv:      oklch(97% 0.003 100);  /* #F7F7F5 — text on orange/dark */

  /* Structure */
  --pr-orange:        oklch(57% 0.205 38);   /* #E84E08 — the structural colour */
  --pr-orange-dim:    oklch(57% 0.205 38 / 0.08); /* orange tint at 8% opacity */

  /* Borders */
  --pr-border:        oklch(13% 0.005 60);   /* #1A1814 — primary 2px border */
  --pr-border-mid:    oklch(80% 0.006 100);  /* #C8C4BE — card borders */
  --pr-border-light:  oklch(88% 0.005 100);  /* #E0DCD6 — subtle row dividers */
}
```

**Colour role rules:**
- `--pr-orange` is used for: nav background, primary CTA background, active filter
  fill, section accent left-border (4px), active nav underline. Never for: text
  colour on white, decorative backgrounds, hover states on non-interactive elements.
- `--pr-surface-dark` is used for: text on orange surfaces, primary CTA text when
  inverted, nav link text on orange band.
- No additional colours are introduced at the project level without triggering a
  rune version review.

## 06 — Typography

```css
@import url('https://fonts.googleapis.com/css2?family=Syne:wght@700;800&family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500&family=JetBrains+Mono:wght@400;500&display=swap');

--pr-font-display: 'Syne', sans-serif;
--pr-font-body:    'DM Sans', sans-serif;
--pr-font-mono:    'JetBrains Mono', monospace;
```

| Element | Font | Weight | Size | Tracking | Leading |
|---|---|---|---|---|---|
| H1 hero | Syne | 800 | clamp(32px, 6vw, 72px) | -0.04em | 0.92 |
| H2 section | Syne | 800 | clamp(22px, 3.5vw, 40px) | -0.03em | 0.95 |
| H3 card | Syne | 700 | 16px | -0.02em | 1.1 |
| Body large | DM Sans | 300 | 15px | 0 | 1.75 |
| Body | DM Sans | 400 | 13px | 0 | 1.65 |
| UI label | DM Sans | 500 | 11px | 0.02em | 1.4 |
| Nav link | JetBrains Mono | 400 | 9px | 0.10em | — |
| Eyebrow | JetBrains Mono | 400 | 9px | 0.18em | — |
| Tag / badge | JetBrains Mono | 400 | 8px | 0.08em | — |
| Metric / data | JetBrains Mono | 500 | contextual | -0.02em | 1 |
| Caption | DM Sans | 400 | 11px | 0.02em | 1.5 |

**Typography rules:**
- Syne 800 is never used below 14px.
- Eyebrows and nav links are always uppercase. Body copy is never uppercase.
- JetBrains Mono appears for: nav links, eyebrow labels, tags and badges, all
  numeric data, metadata captions. Never for body copy or headings.
- One weight distinction signals hierarchy — DM Sans 300 for description, 400 for
  UI, 500 for emphasis. Never 600 or 700 in DM Sans.
- The italic form of Syne (if used) is reserved for pull quotes only. No italic
  in UI chrome.

**FORBIDDEN:** Inter, Roboto, Manrope, Outfit, Plus Jakarta Sans, any system-ui
fallback as a primary font. These signal generic SaaS. A builder encountering
any of these must replace them before delivering.

## 07 — Spatial

```
Base unit:           4px
Page margins:        40px desktop · 20px mobile
Section padding:     72px vertical desktop · 48px vertical mobile
Component padding:   16px standard · 24px card internal
Border weight:       2px all borders — never 1px, never 0.5px
Border radius:       0 — no exceptions
Gap (grid):          8px tight · 16px standard · 24px loose
Max content width:   1200px
Text column max:     680px
```

**Spatial rules:**
- Borders carry depth, not shadows. Two elements separated by a 2px border at 0
  radius read as stacked physical objects.
- No `box-shadow` on interactive elements except focus rings. Focus rings use:
  `outline: 2px solid var(--pr-orange); outline-offset: 2px`.
- Section backgrounds alternate: `--pr-bg` → `--pr-surface-mid` → `--pr-bg`.
  No section uses `--pr-surface` (white) as its full background — white is
  reserved for cards elevated within sections.

## 08 — Motion

Press motion is mechanical, not organic. Type pressed into paper. No spring
physics. No ease-out-back. Transitions snap.

### Named Moments

**Press Mark** — The structural entry.
```
Trigger:   Page / component first mount
Effect:    The orange nav band wipes in from left to right
Timing:    280ms · linear
CSS:       clip-path: inset(0 100% 0 0) → inset(0 0% 0 0)
Semantic:  The mark is applied. The tool is ready.
Use:       Nav only, on first load. Never on route changes.
```

**Hard Land** — Element entrance.
```
Trigger:   Any content block entering the viewport
Effect:    translateY(-6px) opacity 0 → translateY(0) opacity 1
Timing:    160ms · cubic-bezier(0.0, 0.0, 0.2, 1) — hard deceleration
           No ease-in. Instant start, hard stop. Like type dropped on surface.
Semantic:  Content arrives, it does not drift.
Use:       Section headers, card grids on scroll entry.
           NOT used on body text — too much motion in reading contexts.
```

**Stamp** — Active state confirmation.
```
Trigger:   Tag / filter button click or active selection
Effect:    scale(0.94) for 80ms → scale(1.0)
Timing:    80ms out · 120ms return · linear both ways
Semantic:  The stamp is pressed. The selection is physical.
Use:       Filter tags, toggle buttons. Never on primary CTAs.
```

### General motion rules

- Easing for all UI transitions not covered by named moments:
  `cubic-bezier(0.0, 0.0, 0.2, 1)` — instant start, hard deceleration.
  Never `ease-in-out` (too organic) or `ease` (too gentle).
- Duration ceiling: 300ms. Nothing in this rune animates longer than 300ms.
- Hover states: no animation. Colour transitions only — 120ms linear. No border weight change. No transform on hover.
- What must never animate: border-radius (it is always 0), background gradients
  (they do not exist), font-weight (layout shift).

## 09 — Components

### Navigation

```css
nav {
  height: 40px;
  background: var(--pr-orange);
  border-bottom: 2px solid var(--pr-border);
  display: flex;
  align-items: stretch;
}

.nav-brand {
  display: flex;
  align-items: center;
  padding: 0 16px;
  border-right: 2px solid rgba(26,24,20,0.3);
  font-family: var(--pr-font-display);
  font-size: 14px;
  font-weight: 800;
  color: var(--pr-text-inv);
  letter-spacing: -0.02em;
  gap: 8px;
}

.nav-link {
  font-family: var(--pr-font-mono);
  font-size: 9px;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: rgba(247,247,245,0.45);
  padding: 0 12px;
  border-left: 2px solid rgba(26,24,20,0.25);
  display: flex;
  align-items: center;
  height: 100%;
}
.nav-link:hover { color: var(--pr-text-inv); }
.nav-link.active {
  color: var(--pr-text-inv);
  background: rgba(0,0,0,0.12);
}

.nav-cta {
  font-family: var(--pr-font-mono);
  font-size: 9px;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--pr-orange);
  background: var(--pr-border);
  padding: 0 14px;
  border-left: 2px solid rgba(26,24,20,0.4);
  display: flex;
  align-items: center;
}
```

### Buttons

```css
/* Primary */
.btn-primary {
  font-family: var(--pr-font-mono);
  font-size: 9px;
  font-weight: 500;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  background: var(--pr-border);      /* #1A1814 */
  color: var(--pr-text-inv);
  padding: 10px 20px;
  border: 2px solid var(--pr-border);
  border-radius: 0;
  cursor: pointer;
  transition: background 120ms linear;
}
.btn-primary:hover { background: var(--pr-orange); border-color: var(--pr-orange); }
.btn-primary:active { transform: translateY(1px); }

/* Ghost */
.btn-ghost {
  font-family: var(--pr-font-mono);
  font-size: 9px;
  font-weight: 500;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  background: transparent;
  color: var(--pr-text);
  padding: 9px 19px;
  border: 2px solid var(--pr-border);
  border-radius: 0;
  cursor: pointer;
}
.btn-ghost:hover { background: var(--pr-orange-dim); border-color: var(--pr-orange); color: var(--pr-orange); }

/* On orange background (nav CTA) */
.btn-on-orange {
  background: var(--pr-border);
  color: var(--pr-orange);
  /* same structure as primary */
}
```

### Cards

```css
.card {
  background: var(--pr-surface);
  border: 2px solid var(--pr-border);
  border-radius: 0;
  padding: 20px 24px;
  transition: border-color 120ms linear;
}
.card:hover { border-color: var(--pr-text); }

/* Section card (on --pr-surface-mid background) */
.card-section {
  background: var(--pr-surface);
  border: 2px solid var(--pr-border-mid);
  border-radius: 0;
  padding: 20px 24px;
}
.card-section:hover { border-color: var(--pr-border); }
```

### Tags and Badges

```css
.tag {
  font-family: var(--pr-font-mono);
  font-size: 8px;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  padding: 3px 8px;
  border: 2px solid var(--pr-border);
  color: var(--pr-text);
  background: transparent;
  border-radius: 0;
  cursor: pointer;
  margin-left: -2px;    /* overlap borders to form a strip */
}
.tag.active {
  background: var(--pr-orange);
  color: var(--pr-text-inv);
  border-color: var(--pr-orange);
  z-index: 1;
  position: relative;
}
.tag:first-child { margin-left: 0; }
```

### Section headers

```css
.section-header {
  padding: 12px 0 10px;
  border-bottom: 2px solid var(--pr-border);
  display: flex;
  align-items: baseline;
  justify-content: space-between;
  margin-bottom: 20px;
}
.section-title {
  font-family: var(--pr-font-display);
  font-size: 18px;
  font-weight: 800;
  letter-spacing: -0.03em;
  color: var(--pr-text);
}
.section-count {
  font-family: var(--pr-font-mono);
  font-size: 9px;
  letter-spacing: 0.1em;
  color: var(--pr-orange);
}
```

## 10 — Anti-Patterns

Before delivering any output generated from this rune, verify that none of the
following are present:

- [ ] Rounded corners on any element → border-radius must be 0 everywhere
- [ ] 1px borders or hairlines → all borders are 2px solid
- [ ] Orange used as a text highlight or badge background on white → orange is structural only
- [ ] A second accent colour beyond orange → remove it
- [ ] Dark-first or dark hero section → Press is light-first without exception
- [ ] Soft box-shadow on any element → no box-shadows in this rune
- [ ] Inter, Roboto, Manrope, or any system-ui font → replace with Syne / DM Sans / JetBrains Mono
- [ ] Syne used below 14px → use DM Sans instead
- [ ] Gradient of any kind → not permitted
- [ ] Orange used decoratively (icon colour, illustration fill, underline) → structural use only
- [ ] Spring or ease-in-out easing → use cubic-bezier(0.0, 0.0, 0.2, 1) or linear
- [ ] Animations longer than 300ms → shorten
- [ ] border-radius animated → it is always 0, nothing to animate
- [ ] Body copy in uppercase → uppercase is reserved for labels, tags, and nav only
- [ ] Multiple font weights of DM Sans beyond 300 / 400 / 500 → remove heavier weights
- [ ] Display text clamp value exceeding 4vw for a single-word headline → reduce to clamp(32px, 4vw, 64px) and add overflow: hidden to the container

## 11 — Routing

**Use Press for:**
- Design tools, reference systems, and developer-facing products that need
  immediate credibility
- Products with a clear point of view that benefit from an assertive visual posture
- Tools that display or compare multiple items where consistent rigid structure
  aids scanning (the border-and-zero-radius grammar creates natural grid anchors)
- Any product that explicitly rejects the rounded-corner SaaS aesthetic as part
  of its positioning
- Light-first contexts where maximum contrast is a priority

**Avoid Press and consider an alternative when:**
- The audience is non-technical or would find the hard edges aggressive — consider
  a warmer editorial direction (future: Parchment-class rune)
- The product requires genuine warmth and care as a primary signal — consider a
  warm-dark direction (future: Foundry-class rune)
- The product is experience-dominant and the interface should become the scene —
  consider a more expressive direction (future: high-Posture rune)
- Long-form reading is the primary use case — the density and border weight of
  Press creates cognitive friction over extended reading sessions
- The brand requires maximum restraint and the interface must nearly disappear —
  consider a Ghost-class rune (future: minimal single-accent direction)
