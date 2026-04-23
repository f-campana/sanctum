# AGENTS.md

## Identity
Sanctum is the compiled wiki repo. It stores the system's durable knowledge,
indexes, design identity library, and source archives.

## Authorised actions
- Agents may create and edit compiled wiki content outside `40 Sources/`.
- Agents may read from `40 Sources/` but must not modify it.
- Agents may append to `01 Indexes/log.md` when recording completed operations.
- Do not collapse Sanctum and Bifrost into one repo.

## Quality gate
Phase 0 uses human review plus `git diff --check` before anything is considered
complete.

## Skill loading
No repo-local skills are loaded yet. Use the Bifrost design skills once they are
present and referenced by the system spec.

## Context boot
Read in this order:
1. `system-spec.md`
2. `README.md`
3. `01 Indexes/index.md`
4. `01 Indexes/log.md`
5. `10 Knowledge/Design/routing-guide.md`
6. `10 Knowledge/Design/design-principles.md`
7. `40 Sources/Design/sessions/design-pipeline-session-2026-04-22.md`

## Feedback channel
Write harness feedback to `00 Inbox/harness-feedback.md`.

