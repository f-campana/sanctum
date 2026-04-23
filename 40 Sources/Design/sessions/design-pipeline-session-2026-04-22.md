# Session Summary — Design Pipeline + System Spec v0.3

**Date:** 2026-04-21 → 2026-04-22
**Duration:** Extended session (~12 hours)
**Status:** Ready for Sanctum ingestion
**Target location:** `Sanctum/40 Sources/Design/sessions/design-pipeline-session-2026-04-22.md`

---

## What this session was

A deep research and design session that produced the complete specification for the
system's design pipeline domain — the first domain to complete the full
research → model → validate → spec cycle. The session also updated the system-spec
to v0.3, established the naming vocabulary, and produced the first original Rune
in the library.

This document is the authoritative record of decisions made. The raw conversation
is the source for any disputed details.

---

## Decisions made — confirmed and locked

### System vocabulary

The following terms are canonical. Do not substitute synonyms.

| Term | Definition | Register | Lives in |
|---|---|---|---|
| **Sanctum** | The compiled knowledge wiki — private git repo | Infrastructure (Norse/Marvel) | `~/Documents/sanctum/` |
| **Bifrost** | The schema and operating system for agents — public git repo | Infrastructure (Norse/Marvel) | `~/Documents/bifrost/` |
| **Runestone** | The browsable web interface to the Rune library | Infrastructure (Norse/Marvel) | Built in Phase 1 |
| **Rune** | A named, versioned design identity. Not a Design Contract. | Design domain | `Sanctum/10 Knowledge/Design/runes/` |
| **Design Contract** | Project-specific executable file instanced from a Rune | Design domain | `DESIGN_[PROJECT].md` at project root |
| **Axes** | Eight visual/perceptual dimensions used to score every Rune | Design domain | Defined in design-pipeline-contract.md |
| **Moments** | Named, timed animation events that are part of a Rune's identity | Design domain | Section 08 of each Rune file |
| **Routing Guide** | Six-question structured decision tree for Rune selection | Design domain | `Sanctum/10 Knowledge/Design/routing-guide.md` |
| **Run Report** | Structured output from design/builder documenting what happened | Design domain | `Sanctum/00 Inbox/run-report-[date].md` |
| **Promote Gate** | The human review step before any agent output reaches the wiki | Operational | Described in system-spec §17 |
| **Loop-back** | Quality gate wrapper that retries agents on failure before escalating | Operational | `Bifrost/scripts/loop-back.sh` |
| **Domain Deepening** | The pattern: research → model → validate → spec, applied per domain | Operational | Described in system-spec §06 |
| **Press** | The first original Rune in the system | Rune name | `Sanctum/10 Knowledge/Design/runes/press.md` |

**Note on language:** The entire system uses English throughout. No French
except in product names that are inherently French (FODMAPP). No borrowings
from Ropau's naming system.

**Note on Codex (OpenAI):** The name "Codex" is reserved — OpenAI's tool uses
this name and we use it extensively as an agent harness. It must not be used
as a system component name. This is why the signature library interface was
named Runestone, not Codex.

---

### Design pipeline architecture

**Three-layer model — confirmed:**
- Layer 1: Rune (emotional + visual identity, lives in Sanctum, reusable)
- Layer 2: Design Contract (project-specific instance, lives at project root)
- Layer 3: Skills in Bifrost (curator, builder, validator, dialogue, harvester, distill)

**Key architectural decisions:**
- design/builder reads the Design Contract only — the Rune is not a runtime
  dependency for the builder. The DESIGN file must be self-contained.
- Routing is human. design/curator never selects a Rune autonomously. The
  Routing Guide is a reference the human consults before dispatching curator.
- OKLCH with two-letter namespace prefixes from the start, not hex. No migration.
  Press namespace: `--pr-`. Convention: two letters from the Rune slug.
- Canonical copy lives in the Design Contract, not the Rune. Runes have no
  canonical copy section — that's a Ropau-specific feature for their own brand.
- The Runestone is not deferred. Phase 1 deliverable. It validates the pipeline
  by being the first project the pipeline runs on (dogfood).

**The eight axes — fixed names and pole labels:**
Density · Temperature · Luminosity · Energy · Geometry · Chromatism · Depth · Posture
Each axis scored 1–10. Each score has a one-sentence written interpretation
specific to how that Rune expresses it.

**Token format:**
```css
--[namespace]-[token-name]: oklch([L%] [C] [H]);  /* #hex as secondary ref */
```

**Rune version semantics:**
- patch (0.0.x): wording, examples, minor values — no visual change
- minor (0.x.0): new component rules, colour adjusted within same hue
- major (x.0.0): archetype changes, test sentence changes, axis shifts >2,
  new inviolable rule. Triggers re-instancing of all affected Design Contracts.

---

### The domain-deepening pattern — confirmed as a core system principle

Every technical domain starts lightweight (SKILL.md only) and earns a full
contract through real use. The trigger for deep investment: agent failures that
are specific, recurring, and consequential.

**Four stages:**
1. Research — study who has already solved this rigorously
2. Model — name things precisely with vocabulary that fits the system register
3. Validate — run real work through lightweight specs, observe specific failures
4. Spec — write the contract from evidence, not theory

Design is the first domain to complete all four stages. Other domains (frontend,
TypeScript, backend, database, testing) follow when they qualify.

The design pipeline is not a special case. It is the template.

---

### Press — the first original Rune

**Name:** Press
**Slug:** `press`
**Namespace:** `--pr-`
**Archetypes:** Creator + Outlaw
**Radar:** `6-4-8-8-9-2-4-7`
**Status:** Stable v1.0.0
**Test sentence:** "Does this look like it was printed by someone who knows
exactly what they're doing?"

**The five inviolable rules:**
1. Orange (`oklch(57% 0.205 38)` / `#E84E08`) is structural only — never decorative
2. `border-radius: 0` everywhere — no exceptions
3. All borders `2px solid` — never 1px, never 0.5px
4. Light-first always — no dark-mode variant, no dark hero sections
5. One structural colour only — no second accent

**Three named motion moments:**
- Press Mark: nav band wipes left-to-right on first mount, 280ms linear
- Hard Land: elements enter at translateY(-6px) → 0, 160ms hard deceleration
- Stamp: filter tags scale(0.94) on click, 80ms, physical press feel

**Known gaps to address before first builder run:**
- Input and form element specs not yet written (needed for Runestone search)
- Route-change transition not specified (only first-mount is defined)

**First project:** Runestone. The Runestone instances Press via design/curator
to produce its own Design Contract — first real dogfood run of the pipeline.

---

### Intellectual property boundary — important

Argent Décisif, Néon Humaniste, Signal Brut, Encre Éditoriale, Aube Opérative,
Cristal Cartographique, Encre Souveraine, Flux Bienveillant, Prisme Analytique,
Toile Narrative, Crimson Rain — these are Ropau's design identities from their
Design Forge system. They must not appear in our system as our own Runes.

What we derived from studying their system:
- The methodology (brief → signature → contract → build → harvest → distill)
- The eight visual axes concept (we named and defined our own eight)
- The named motion moments concept
- The routing governance concept
- The inviolable rules as decision trees concept

What belongs to them and must not be replicated:
- All named Rune identities listed above
- Their specific radar vocabulary and scoring system
- Their canonical copy phrases
- Their specific token values and visual expressions

Our system's design methodology is original. Our Rune library starts with Press
and grows from real project use.

---

### Sources consulted in this session

**Ropau / Powlisher (Paul + Robin):**
- Design Forge screenshots (Crimson Rain, Calme Dense, Néon Humaniste pages)
- Design Forge gallery (eleven signatures overview)
- Design Forge routing guide (/guide page)
- Two video transcripts from their live streams

**Emil Kowalski:**
- animations.dev course site — SKILL.md for animations, motion grammar
- "Agents with Taste" article — taste-encoding methodology, decision trees

**Google:**
- google-labs-code/design.md repository and spec
- CLI tools: lint, diff, tailwind export
- Token schema (YAML frontmatter standard)

**Key insights from external sources:**
- Google: YAML frontmatter + markdown body as the dual-layer format.
  `npx @google/design.md lint` as first validation step in design/validator.
- Emil: decision trees over preference lists. Motion is archetype-expression,
  not polish. Taste is articulable and packagable as a skill.
- Ropau: the signature as a living queryable artifact (not just a document).
  The Guide de Choix as a routing mechanism. Motion tokens as first-class
  design tokens. The eight visual axes as directly executable CSS decisions.

---

## What was produced

| Artifact | Location | Status |
|---|---|---|
| `design-pipeline-contract.md` | `Bifrost/contracts/` | Complete |
| `press.md` | `Sanctum/10 Knowledge/Design/runes/` | Complete — two known gaps |
| `system-spec.md` v0.3 | `Bifrost/` | Complete |
| `system-spec.html` v0.3 | `Bifrost/` | Complete |
| Signal Brut landing page package | Validated against cold instance | Prior art only |
| Chapitre landing page package | Validated against cold instance | Prior art only |
| Trame landing page package | Validated against cold instance | Prior art only |

---

## What was validated

**Design pipeline end-to-end (three cold instances):**
- Brief → Rune selection → Design Contract → cold Claude instance → HTML output
- Three different design identities produced distinct, recognisable outputs
- Signal Brut: cold instance produced yellow hero on first attempt with package v3
- Chapitre: cold instance produced serif headlines throughout, correct copper accent
- Trame: cold instance produced correct cream canvas, coral accent, warm tone

**Key learning from validation runs:**
- Hero composition must be spatially specified (proportions, column content)
- Product preview must be spec'd to element level — no "show the product here"
- Section alternation needs a visual map, not a list
- Inviolable rules work best as decision trees with binary yes/no branches
- The most important anti-pattern to repeat is the one the model fails most
  (Signal Brut needed "yellow hero" stated three times in three files)
- design/builder should be a generic skill — all signature constraints in the
  Design Contract, not in the skill. One skill, all Runes.

---

## Phase 0 build sequence — immediate next actions

In order. Do not skip steps.

**System infrastructure:**
1. `git init` in `~/Documents/sanctum/` (private) and `~/Documents/bifrost/` (public)
2. Scaffold both folder structures per system-spec §4 and §5
3. Create `Sanctum/01 Indexes/log.md` — empty but present from day one
4. Create all templates in `Sanctum/99 Templates/` including `rune.md`
5. Symlink `bifrost/skills/` → `~/.agents/skills/bifrost/`
6. Install Ollama on Mac mini — first model running (GLM-4.7-Flash or Qwen2.5-Coder:7b)
7. Pi on Mac mini — manual dispatch proven once

**Design domain — commit this session's outputs:**
8. Commit `press.md` to `Sanctum/10 Knowledge/Design/runes/press.md`
9. Commit this session summary to `Sanctum/40 Sources/Design/sessions/`
10. Write `Sanctum/10 Knowledge/Design/routing-guide.md`
11. Write `Sanctum/10 Knowledge/Design/design-principles.md`
12. Write `Bifrost/skills/design/design-curator/SKILL.md`
13. Write `Bifrost/skills/design/design-builder/SKILL.md`
14. Write `Bifrost/skills/design/design-validator/SKILL.md`

**First run:**
15. Write `DESIGN_RUNESTONE.md` manually from Press rune (design/curator not yet built)
    This is the first Design Contract. It validates the rune file before an agent
    touches it and surfaces the two known gaps (inputs, route transitions).

---

## Open items — not blocking Phase 0

These were discussed but not resolved. Address after first real runs.

- **Naming dictionary / system glossary:** Agreed it should exist at
  `Sanctum/10 Knowledge/Concepts/system-glossary.md`. Not written yet.
  Vocabulary that survives implementation is vocabulary worth defining.

- **system-spec styled in Press:** The system-spec.html should be rebuilt using
  a Design Contract instanced from Press. Deferred until design/curator exists
  so the process is demonstrated correctly. Do not manually style it with borrowed
  aesthetics (Blade, Ghost are not our Runes).

- **Press rune gaps:**
  - Input/form element component spec (needed for Runestone)
  - Route-change transition spec (currently undefined)
  Address as patch 1.0.1 before first design/builder run on Runestone.

- **Runestone technical stack decision:** Next.js App Router vs Astro.
  Not yet decided. Decide at Phase 1 start based on content dynamism needs.

---

## Things to not repeat

From the validation runs and the iterative design work in this session:

- Do not generate placeholder Rune libraries with borrowed identities. One
  real original Rune is worth more than twelve borrowed ones.
- Do not write design SKILL.md files with signature-specific guards baked in.
  Generic skill + rich Design Contract is the correct separation.
- Do not defer the Runestone. Building the pipeline without a real project
  to run it on is building in a vacuum.
- Do not begin other domain contracts (frontend, backend) before running real
  work through the lightweight skills that already exist. Wait for specific,
  recurring, consequential failures.
- Do not use Codex, OpenAI Codex, or any variation as a system component name.

---

*Session summary complete. Ingest into Sanctum/40 Sources after human review.*
