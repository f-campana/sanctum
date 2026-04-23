# System Glossary

**Location:** `Sanctum/10 Knowledge/Concepts/system-glossary.md`
**Version:** 1.0.0
**Status:** Evergreen — update when new terms are introduced or definitions change
**Last updated:** 2026-04-22

This glossary defines every term used across Sanctum, Bifrost, and all agent
contracts. Definitions are canonical for vocabulary and naming. When a term
here conflicts with usage elsewhere in the system, update the conflicting
document to match this glossary — unless a system-spec update has introduced
a newer definition, in which case update this glossary first.

Terms are grouped by register. Within each group, alphabetical order.

---

## Infrastructure (Norse/Marvel register)

These names follow the Norse/Marvel register established at system inception.
New infrastructure components should fit this register.

---

### Bifrost

**What it is:** The public git repository containing all agent operating
instructions. Owns skills, contracts, routing rules, quality gate scripts, and
prompt assembly rules. Tells agents how to behave. Does not contain knowledge.

**What it is not:** Not a knowledge base. Not a wiki. Not a product. Bifrost
defines how Sanctum is maintained and how agents operate — it does not contain
what the system knows. If you are unsure whether something belongs in Bifrost
or Sanctum, ask: does this define behaviour or encode knowledge? Behaviour →
Bifrost. Knowledge → Sanctum.

**Lives in:** `~/Documents/bifrost/` (public repo)

**Relates to:** Sanctum (the knowledge base Bifrost governs)

---

### Runestone

**What it is:** The browsable web interface to the Rune library. Renders each
Rune as a live experience — type specimens, colour swatches, motion moment
previews, radar visualisation, routing guide. The primary tool for selecting
a Rune before dispatching design/curator. Built using the design pipeline itself
(dogfood principle).

**What it is not:** Not a documentation site. Not a Storybook. Not a design
system viewer. The Runestone is an experiential reference — you use it to feel
the difference between Runes, not just read about them.

**Lives in:** Deployed web application (Phase 1). Local development at
`localhost:3100`.

**Relates to:** Rune (what it displays), design/dialogue (the conversational
alternative before Runestone exists), Routing Guide (the selection flow at
`/guide`)

---

### Sanctum

**What it is:** The private git repository containing all compiled system
knowledge. Owns sources, synthesis, memory, indexes, project context, and the
design identity library. Maintained by agents, read by both humans and agents.
Knowledge compounds here over time through the ingest and distill loops.

**What it is not:** Not the operating instructions for agents (that is Bifrost).
Not a task management system. Not a place for transient work — anything in
Sanctum is either a durable knowledge artifact or a source awaiting ingestion.

**Lives in:** `~/Documents/sanctum/` (private repo)

**Relates to:** Bifrost (the schema that governs Sanctum), Promote Gate (the
human review step before output reaches durable Sanctum zones)

**Two zones:**
- Immutable zone (`40 Sources/`) — raw inputs, LLM reads but never modifies
- Compiled zone (everything else) — LLM-maintained, compounds over time

---

## Design Domain

These terms are specific to the design pipeline. All English. No French except
in inherently French product names.

---

### Axes

**What it is:** The eight visual/perceptual dimensions used to score every Rune.
Each axis has a name, two pole labels, and a score (1–10) per Rune. Each score
is accompanied by a one-sentence written interpretation specific to how that
Rune expresses it. Axis scores are directly executable as CSS decisions — no
intermediate translation required.

**What it is not:** Not emotional descriptors (that is the Archetype system).
Not subjective impressions. Not style preferences. The axes are a measurement
system that produces deterministic design decisions.

**The eight axes:**

| Axis | Low pole | High pole |
|---|---|---|
| Density | Airy | Dense |
| Temperature | Cold | Warm |
| Luminosity | Dark-first | Light-first |
| Energy | Static | Expressive |
| Geometry | Organic | Geometric |
| Chromatism | Monochrome | Polychrome |
| Depth | Flat | Layered |
| Posture | Utility | Experience |

**Lives in:** Section 03 of each Rune file. Defined authoritatively in
`Bifrost/contracts/design-pipeline-contract.md`.

**Relates to:** Rune (where axes are scored), Archetype (the complementary
emotional system)

---

### Archetype

**What it is:** A Carol Pearson archetype label assigned to a Rune (1–2 per
Rune). Governs the cultural and psychological register — the *why* behind
visual decisions. The archetype answers: what does this product believe about
the world? Archetypes are a pointer into a shared cultural vocabulary, not a
measurement system.

**What it is not:** Not a score. Not a visual specification. Not interchangeable
with the Axes system. Archetypes produce creative direction; Axes produce CSS
values. Both are required; neither replaces the other.

**The twelve archetypes (Carol Pearson):**
Innocent · Explorer · Sage · Hero · Outlaw · Magician ·
Regular Person · Lover · Jester · Caregiver · Creator · Ruler

**Lives in:** YAML frontmatter of each Rune file (`archetypes:` field).
Section 02 of each Rune file.

**Relates to:** Rune (where archetypes are assigned), Axes (the complementary
visual measurement system)

---

### Design Contract

**What it is:** The project-specific, agent-executable file instanced from a
Rune for a given project. Lives at the project root as `DESIGN_[PROJECT].md`.
Contains YAML frontmatter (Google `design.md` spec compliant) and a markdown
body with all constraints an agent needs to execute the design. Complete and
self-contained — design/builder reads only this file, not the source Rune.

**What it is not:** Not a Rune. A Design Contract is a project-specific
instance derived from a Rune. The Rune is reusable; the Design Contract is
not. Not a style guide. Not a Figma file. Not a brief — the brief is an input
to design/curator which produces the Design Contract.

**Format:** `DESIGN_[PROJECT].md` at project root.
Examples: `DESIGN_RUNESTONE.md`, `DESIGN_[PROJECT].md`

**Lives in:** Project repository root.

**Relates to:** Rune (the source it is instanced from), design/curator (the
skill that creates it), design/builder (the skill that reads it)

---

### Inviolable Rules

**What it is:** 3–5 binary, testable visual conditions defined in a Rune that,
if any one is absent, mean the output is not that Rune. Written as decision
trees with explicit yes/no branches, not as prose preferences. Checked
mechanically by design/validator.

**What it is not:** Not suggestions. Not preferences. Not guidelines. If an
output violates an inviolable rule, the run has failed and must be corrected
before delivery.

**Format:** Decision tree with binary branches.
```
Is border-radius: 0 on every element?
  Yes → proceed
  No  → STOP. Fix before continuing.
```

**Lives in:** Section 04 of each Rune file. Reproduced verbatim in the Design
Contract's `## Inviolable Rules` section.

**Relates to:** Rune (where they are defined), Design Contract (where they are
reproduced), design/validator (which checks them)

---

### Moments

**What it is:** Named, timed animation events that are part of a Rune's
identity. 2–5 per Rune. Each moment expresses a specific aspect of the
archetype profile through motion. Not decorative polish — semantic expression.
Each moment has: a name, a trigger, timing (duration + easing), CSS
specification, semantic meaning, and exclusive use context.

**What it is not:** Not generic animation guidelines (those live in
`Sanctum/10 Knowledge/Design/design-principles.md`). Not micro-interactions
(hover states, focus rings). Moments are named, brand-specific, archetype-
expressive animation events — the equivalent of a signature move.

**Example (from Press):**
- Press Mark — nav band wipes left to right on first mount, 280ms linear
- Hard Land — elements enter translateY(-6px) → 0, 160ms hard deceleration
- Stamp — filter tags scale(0.94) on click, 80ms physical press feel

**Lives in:** Section 08 of each Rune file. Inherited by the Design Contract's
`## Motion` section.

**Relates to:** Rune (where they are defined), Design Contract (where they are
inherited), design/builder (which implements them)

---

### Routing Guide

**What it is:** A six-question structured decision tree in Sanctum for selecting
the right Rune for a given brief. Questions are ordered deliberately: audience
→ posture → register → density → luminosity → sector. The first three eliminate
the majority of candidates. The last three discriminate between the remaining
1–3. Each answer links to qualifying Runes.

**What it is not:** Not an agent step. Routing is a human decision. The Routing
Guide is a reference the human consults before dispatching design/curator.
design/curator never selects a Rune autonomously.

**Lives in:** `Sanctum/10 Knowledge/Design/routing-guide.md`. Also accessible
at `/guide` in the Runestone (Phase 1).

**Relates to:** Rune (what it routes to), design/curator (which is dispatched
after routing), Runestone (which renders it interactively)

---

### Run Report

**What it is:** A structured markdown file produced by design/builder alongside
every HTML output. Documents: which Rune was used, which Design Contract
version, which sections were generated, which anti-patterns were detected and
suppressed, which inviolable rules were verified, test sentence result, and
any notes. The primary input to design/harvester.

**What it is not:** Not a log entry (that is `log.md`). Not a validation
report (that is produced by design/validator). The Run Report is design/
builder's own account of what it did.

**Format:** `run-report-[YYYY-MM-DD].md`

**Lives in:** `Sanctum/00 Inbox/` pending promote gate review.

**Relates to:** design/builder (which produces it), design/harvester (which
reads it), design/validator (the separate validation output)

---

### Rune

**What it is:** A named, versioned design identity. Encodes visual DNA, motion
system, routing governance, and the annotated radar for a specific archetype
profile. Lives permanently in Sanctum. Reusable across multiple projects that
share the same archetype profile. The source from which Design Contracts are
instanced. Versioned with semver.

**What it is not:** Not a Design Contract. A Rune is the reusable template;
a Design Contract is the project-specific instance derived from it. Not a
style guide or design system. Not a component library. Not borrowed from
external systems — all Runes in this system are original, authored from
real briefs, validated through real runs.

**Format:** `[slug].md` with YAML frontmatter and eleven required sections.

**Lives in:** `Sanctum/10 Knowledge/Design/runes/[slug].md`

**Current library:** Press v1.0.0 (`press.md`, namespace `--pr-`)

**Relates to:** Design Contract (the project-specific instance), Runestone
(the browsable interface), Axes and Archetypes (the measurement systems),
Moments (the motion layer), design/curator (which instances it)

---

## Operational Terms

These terms describe how the system operates. Register: plain English,
precise, no metaphor.

---

### Compiled Zone

**What it is:** All of Sanctum except `40 Sources/`. The zone the LLM owns
and maintains. Agents create, update, and cross-reference content here.
Everything in this zone has been processed and synthesised from raw sources.

**What it is not:** Not immutable. Not raw. The compiled zone is the output
of the system's intelligence — it changes as understanding improves.

**Lives in:** Sanctum — all folders except `40 Sources/`

**Relates to:** Immutable Zone (the counterpart), Promote Gate (the gateway
between agent output and durable compiled zone content)

---

### Domain Deepening

**What it is:** The four-stage process by which a technical domain in the
system is elevated from a lightweight skill to a full specced contract.
Stages: Research → Model → Validate → Spec. Triggered when agent failures
in a domain become specific, recurring, and consequential.

**What it is not:** Not applied to every domain upfront. Not planning. The
trigger is observed failure, not anticipated need. A domain earns the deep
process through evidence.

**The four stages:**
1. Research — study who has solved this rigorously, learn from them
2. Model — name things precisely with vocabulary that fits the system
3. Validate — run real work through lightweight specs, observe what breaks
4. Spec — write the contract from evidence, not theory

**Current status:** Design is the first completed domain. All other domains
start as lightweight SKILL.md files until they qualify.

**Lives in:** `Bifrost/system-spec.md` §06 (definition). Contracts produced
by the process live in `Bifrost/contracts/`.

**Relates to:** SKILL.md (the lightweight starting point), Contract (the
full-spec end state)

---

### Dogfood

**What it is:** The principle that each phase uses what was built in the
previous phase. The system builds itself. Concretely: the design pipeline
is used to build the Runestone. The wiki/ingest skill is used to file the
notes from its own creation. The GitHub write skills are tested by opening
a PR for themselves.

**What it is not:** Not a metaphor — it is a quality gate. If a new capability
cannot be used to validate itself, it is not ready to be used on external work.

**Relates to:** Phase Sequence (where dogfood targets are specified per phase)

---

### Harvest Report

**What it is:** A structured markdown document produced by design/harvester
after reviewing a batch of Run Reports. Identifies patterns: anti-pattern
rules that are repeatedly violated (candidates for stronger wording), sections
that consistently required manual correction, emerging patterns not covered by
the current Rune. A proposal document — it does not modify anything.

**What it is not:** Not a Run Report (which is per-run, from design/builder).
Not a validation report. The Harvest Report is a meta-analysis across multiple
runs.

**Format:** `harvest-[YYYY-MM-DD].md`

**Lives in:** `Sanctum/00 Inbox/` pending human review.

**Relates to:** Run Report (its input), design/distill (which acts on approved
findings), Rune (which is updated as a result)

---

### Immutable Zone

**What it is:** `Sanctum/40 Sources/` — raw input material that agents read
but never modify. All source material retains provenance here. If a source
contains an error, the error stays in the immutable zone permanently and the
correction lives in the compiled zone.

**What it is not:** Not a place to store agent output. Not a staging area.
Once something is filed in the immutable zone, it stays.

**Lives in:** `Sanctum/40 Sources/`

**Relates to:** Compiled Zone (the counterpart), wiki/ingest (the skill that
reads from it)

---

### Inbox

**What it is:** `Sanctum/00 Inbox/` — the staging area where all agent output
lands before human review. Every skill that produces a durable artifact writes
to the Inbox first. Nothing in the Inbox is promoted to the compiled zone
without the human reviewing it.

**What it is not:** Not a permanent storage location. The Inbox is a queue,
not an archive. Files that are approved move to their target location.
Files that are rejected are discarded.

**Lives in:** `Sanctum/00 Inbox/`

**Relates to:** Promote Gate (the review process that clears the Inbox),
Run Report (a typical Inbox resident), Harvest Report (a typical Inbox resident)

---

### Log

**What it is:** `Sanctum/01 Indexes/log.md` — an append-only chronological
record of all system operations. Every significant agent action gets an entry:
ingest runs, design runs, query responses that became wiki pages, lint passes,
skill creations. The log is never edited — only appended.

**What it is not:** Not a task list. Not a changelog for the Bifrost codebase
(that is `docs/changelog`). The log records what happened in the system,
not what changed in the code.

**Format per entry:**
`## [YYYY-MM-DD] skill-id | brief description of what happened`

**Lives in:** `Sanctum/01 Indexes/log.md`

**Relates to:** wiki/ingest (which writes entries), design/builder (which
writes entries), all skills with durable output (which write entries)

---

### Loop-back

**What it is:** The quality gate wrapper script that runs around every agent
invocation. Captures the exit code from the quality gate. On exit 0, the
output moves to Inbox for human review. On exit 1, structured feedback JSON
is prepended to the agent prompt and the agent retries (maximum 3 times).
After 3 failures, escalates to the human with the failure JSON.

**What it is not:** Not the quality gate itself (that is `quality-gate.sh`).
Not a retry loop without structure — each retry includes the specific failure
feedback so the agent can correct, not just try again blindly.

**Lives in:** `Bifrost/scripts/loop-back.sh` (~50 lines). Built in Phase 2.

**Relates to:** Quality Gate (which the loop-back invokes), Inbox (where
passing output lands)

---

### Promote Gate

**What it is:** The human review step that governs all movement from
`Sanctum/00 Inbox/` to the durable compiled zone. Agent writes to Inbox →
human opens, reads, decides. Three outcomes: approve (move to target
location), reject (discard), partial approve (edit inline then move).
Nothing reaches `10 Knowledge/` or `30 Memory/` without human review.

**What it is not:** Not automated. Not delegatable to an agent. The Promote
Gate is the human's point of control over what the system knows. It is also
the self-improvement gate: Rune updates proposed by design/distill, wiki
updates proposed by wiki/ingest, all pass through the Promote Gate.

**Relates to:** Inbox (the queue it clears), Compiled Zone (the destination
it gates), Loop-back (the preceding automated quality step)

---

### Pull Before Push

**What it is:** The principle that every automated trigger starts as manual
dispatch. A skill earns automated triggering only after ≥2 weeks of
predictable manual use with no failures. Automation is a reward for proven
reliability, not a default.

**What it is not:** Not a permanent state. Manual dispatch is the starting
position; automation is the destination for reliable skills. Not a rule
against automation — it is a rule against premature automation.

**Relates to:** Phase Sequence (Phase 8 introduces webhook triggers after
all prior phases have proven manual reliability)

---

### Quality Gate

**What it is:** `Bifrost/scripts/quality-gate.sh` — a shell script with two
modes. `--llm-only` (fast, <30s): LLM lint surface + TypeScript type check,
produces structured JSON output. `--full`: format + lint + typecheck + tests
+ build + changeset check. The `--llm-only` mode is what the loop-back invokes
on every agent run.

**What it is not:** Not the loop-back (which wraps the quality gate and handles
retries). Not a CI replacement — it runs in CI too, but it also runs locally
on every agent output before the human sees it.

**Lives in:** `Bifrost/scripts/quality-gate.sh`

**Relates to:** Loop-back (which invokes it), LLM lint surface
(`eslint.llm.config.mjs` — promotes agent-relevant warnings to errors)

---

## Naming Conventions

### Register rules

**Infrastructure names** (Sanctum, Bifrost, Runestone) follow the Norse/Marvel
register. New infrastructure components should fit this register. Do not
introduce classical Greek (Atlas), Latin (Codex), or generic English
(Repository, Store, Hub) into infrastructure naming.

**Domain terms** (Rune, Design Contract, Axes, Moments, Routing Guide) use
precise English. No French except in inherently French product names.

**Operational terms** (Promote Gate, Loop-back, Inbox, Quality Gate) use plain
English. No register requirement — clarity is the only criterion.

### Reserved names

**Codex** — reserved. OpenAI's agent harness uses this name. Do not use as a
system component name under any circumstance.

**Forge** — reserved. Ropau's design system uses this name publicly. Do not
use as a system component name.

**The Ropau rune names** — Argent Décisif, Néon Humaniste, Signal Brut,
Encre Éditoriale, Aube Opérative, Cristal Cartographique, Encre Souveraine,
Flux Bienveillant, Prisme Analytique, Toile Narrative, Crimson Rain are
Ropau's intellectual property. Do not use as Rune names in this system.

### Capitalisation

- Proper system nouns are capitalised: Sanctum, Bifrost, Runestone, Press,
  Rune, Design Contract, Inbox, Promote Gate, Loop-back, Quality Gate.
- Common usage of these words is lowercase: "a sanctum for knowledge",
  "the inbox in your email app."
- Skill identifiers are never capitalised: `design/curator`, `wiki/ingest`.

---

*End of system glossary v1.0.0*
*This document is evergreen — update when new terms are introduced or
definitions drift from usage.*
