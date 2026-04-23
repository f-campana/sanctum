---
name: Rune Name
slug: rune-slug
version: 1.0.0
status: draft           # draft | stable | deprecated
archetypes: [Primary, Secondary]
namespace: xx           # two-letter prefix — must be unique across all Runes
radar: "0-0-0-0-0-0-0-0"  # DEN·TEM·LUM·ENE·GEO·CHR·DEP·POS each 1–10
test_sentence: "Does this look/feel like [one sentence that captures the identity]?"
instances: 0
first_instanced: null
---

# Rune Name

## 01 — Essence

Three to five sentences. The emotional and cultural register of this Rune.
Who this is for. What it refuses to be. The test sentence explained. This
is what the human reads to decide if this Rune fits a brief.

## 02 — Archetypes

**[Primary archetype]** (primary) — One paragraph describing specifically
how this archetype manifests visually in this Rune. Not generic archetype
theory — this Rune's specific expression.

**[Secondary archetype]** (secondary) — One paragraph. Same format.

## 03 — Radar

Eight axis scores with one-sentence written interpretation each.
Format: Name · Score — Interpretation specific to this Rune's expression.

```
Density      [1-10]  — [One sentence describing this Rune's specific density expression]
Temperature  [1-10]  — [One sentence]
Luminosity   [1-10]  — [One sentence]
Energy       [1-10]  — [One sentence]
Geometry     [1-10]  — [One sentence]
Chromatism   [1-10]  — [One sentence]
Depth        [1-10]  — [One sentence]
Posture      [1-10]  — [One sentence]
```

## 04 — Inviolable Rules

3–5 binary, testable conditions. If any one fails, the output is not this
Rune. Written as decision trees, not prose preferences.

**Rule 1 — [Rule name].**
```
[Question that can be answered yes or no]?
  Yes → proceed
  No  → STOP. [Specific corrective instruction]. Fix before continuing.
```

**Rule 2 — [Rule name].**
```
[Question]?
  Yes → proceed
  No  → STOP. [Corrective instruction].
```

## 05 — Canvas

All tokens use the `--[namespace]-` prefix.

```css
:root {
  /* Surfaces */
  --[ns]-bg:          oklch([L%] [C] [H]);  /* #hex — role description */
  --[ns]-surface:     oklch([L%] [C] [H]);  /* #hex — role description */
  --[ns]-surface-mid: oklch([L%] [C] [H]);  /* #hex — role description */

  /* Text */
  --[ns]-text:        oklch([L%] [C] [H]);  /* #hex — primary text */
  --[ns]-text-2:      oklch([L%] [C] [H]);  /* #hex — secondary text */
  --[ns]-text-inv:    oklch([L%] [C] [H]);  /* #hex — inverted text */

  /* Accent(s) */
  --[ns]-accent:      oklch([L%] [C] [H]);  /* #hex — role: [structural use] */

  /* Borders */
  --[ns]-border:      oklch([L%] [C] [H]);  /* #hex — primary border */
  --[ns]-border-mid:  oklch([L%] [C] [H]);  /* #hex — secondary border */
}
```

**Colour role rules:** [One sentence per accent defining what it is used
for and what it is never used for.]

## 06 — Typography

```css
--[ns]-font-display: '[Font Name]', sans-serif;
--[ns]-font-body:    '[Font Name]', sans-serif;
--[ns]-font-mono:    '[Font Name]', monospace;
```

| Element    | Font    | Weight | Size               | Tracking  | Leading |
|------------|---------|--------|--------------------|-----------|---------|
| H1 hero    | Display | 800    | clamp(Xpx,Yvw,Zpx) | -0.04em   | 0.92    |
| H2 section | Display | 700    | clamp(Xpx,Yvw,Zpx) | -0.03em   | 0.95    |
| Body       | Body    | 400    | 14px               | 0         | 1.7     |
| Mono label | Mono    | 400    | 9px                | 0.12em    | —       |

**Typography rules:**
- [Rule 1 — minimum size, forbidden combinations, etc.]
- [Rule 2]
- **FORBIDDEN:** [List font families that must never appear in this Rune.]

## 07 — Spatial

```
Base unit:        4px
Page margins:     [X]px desktop · [Y]px mobile
Section padding:  [X]px vertical desktop · [Y]px vertical mobile
Component:        [X]px standard · [Y]px card internal
Border weight:    [X]px
Border radius:    [X]px
Gap scale:        [tight]px · [standard]px · [loose]px
Max content:      [X]px
Text column:      [X]px
```

## 08 — Motion

[Describe the motion philosophy in one sentence. e.g. "Mechanical, not
organic. Hard stops, no spring physics."]

### Named Moments

**[Moment Name]** — [One sentence describing what it expresses.]
```
Trigger:         [What triggers this moment]
Effect:          [CSS description of the animation]
Timing:          [duration · easing]
Semantic:        [What this motion means in the archetype context]
Exclusive use:   [Where this moment appears — and where it must never appear]
```

### General motion rules

- Easing family: [cubic-bezier values or named easing]
- Duration ceiling: [X]ms
- What must never animate: [list]

## 09 — Components

### [Component name]

```css
.[component] {
  /* token-referenced CSS */
}
```
[One sentence: what this component must never do.]

## 10 — Anti-Patterns

Binary checklist. Each item is mechanically checkable.

- [ ] [Anti-pattern] → [correction]
- [ ] [Anti-pattern] → [correction]
- [ ] Generic font stack (Inter, Roboto, system-ui) → replace with Rune fonts

## 11 — Routing

**Use [Rune name] for:**
- [Context 1]
- [Context 2]

**Avoid [Rune name] and consider an alternative when:**
- [Disqualifying context 1] — [which future Rune class would be better]
- [Disqualifying context 2]
