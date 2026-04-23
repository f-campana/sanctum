---
type: session-summary
date: YYYY-MM-DD
thread: claude | codex | other
project: project-name-or-system
status: ready-for-ingest  # draft | ready-for-ingest | ingested
---

# Session Summary — [Brief title of what this session accomplished]

**Date:** YYYY-MM-DD  
**Thread:** [Claude / Codex implementation / other]  
**Duration:** [Approximate — e.g. "2 hours"]  
**Target location:** `Sanctum/40 Sources/[domain]/sessions/[filename].md`

---

## What this session was

One paragraph. The purpose of the session, what was being built or decided,
and why it mattered. Readable without prior context.

---

## Decisions made — confirmed and locked

List every decision that is now canonical. Use this format:

**[Decision name]:** [What was decided and why. One to three sentences.
Enough to understand the reasoning without re-reading the full session.]

---

## Artifacts produced

| Artifact | Target path | Status |
|---|---|---|
| `filename.md` | `Sanctum/path/to/file.md` | committed / pending |
| `filename.md` | `Bifrost/path/to/file.md` | committed / pending |

---

## What was validated

[Optional — only if the session included real runs or tests.]

Describe what was run, against what, and what passed or failed. Be specific.
"Three cold instances produced distinct outputs" is useful.
"Testing went well" is not.

---

## Open items — not blocking current phase

- **[Item]:** [What needs to happen and when.]
- **[Item]:** [What needs to happen and when.]

---

## Things to not repeat

Specific, named mistakes or failure patterns from this session that should
not recur. Written as instructions, not post-mortems.

- Do not [specific action] because [specific reason].
- Do not [specific action].

---

*Session summary ready for ingest into Sanctum/40 Sources/ after human review.*
