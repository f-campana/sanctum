# promote-harvest-frontend-phase-1-2026-05-02

## dispatch summary

Execute a human-authorised Promote Gate event for `sanctum/00 Inbox/harvest-frontend-phase-1-2026-05-02.md`:
- copy the file verbatim to `sanctum/10 Knowledge/Concepts/harvest-frontend-phase-1.md`
- delete the Inbox copy
- verify the promoted file matches `HEAD:00 Inbox/harvest-frontend-phase-1-2026-05-02.md` with an empty diff
- update `sanctum/01 Indexes/index.md` to preserve the removed Inbox row and add the canonical Knowledge row
- classify references to the dated Inbox name and remediate any LIVE references only
- append the `wiki/index-rebuild` log entry for this promotion session
- record the work in this Inbox run report

Human review authorised the promotion. Agent execution performed the file move, reference remediation, indexing, and commit preparation.

## actions taken

- `sanctum/10 Knowledge/Concepts/harvest-frontend-phase-1.md` — added by verbatim copy from the Inbox source, content unchanged.
- `sanctum/00 Inbox/harvest-frontend-phase-1-2026-05-02.md` — deleted after the copy.
- `sanctum/01 Indexes/index.md` — changed the Inbox row to `[removed 2026-05-02]` and added the canonical Knowledge row:
  ```md
  | `sanctum/00 Inbox/harvest-frontend-phase-1-2026-05-02.md` | [removed 2026-05-02] | 2026-05-02 |
  | `sanctum/10 Knowledge/Concepts/harvest-frontend-phase-1.md` | Records frontend phase 1 harvest evidence and proposed rules | 2026-05-02 |
  ```
- `bifrost/skills/frontend/frontend-prose-route/SKILL.md` — updated the Sources reference from the dated Inbox artifact to the canonical Knowledge path.
- `sanctum/00 Inbox/promote-harvest-frontend-phase-1-2026-05-02.md` — created as the required Inbox run report for this promotion dispatch.
- `sanctum/01 Indexes/log.md` — appended the `wiki/index-rebuild` session entry for `phase-1-harvest-promotion`.

## verification commands run with output

```text
$ diff <(git -C sanctum show HEAD:'00 Inbox/harvest-frontend-phase-1-2026-05-02.md') 'sanctum/10 Knowledge/Concepts/harvest-frontend-phase-1.md'
```

Diff result: pass. Output was empty.

```text
$ grep -rn 'harvest-frontend-phase-1-2026-05-02' sanctum/ bifrost/ runestone/ --include='*.md' --include='*.astro' --include='*.css'
sanctum/00 Inbox/frontend-prose-route-skill-creation-2026-05-02.md:132:$ ruby -e 'skill=File.readlines("bifrost/skills/frontend/frontend-prose-route/SKILL.md", chomp: true); harvest=File.readlines("sanctum/00 Inbox/harvest-frontend-phase-1-2026-05-02.md", chomp: true); css=File.readlines("runestone/src/styles/press-prose.css", chomp: true); expected_op=harvest[297,5]; idx=skill.index("Operating rules:"); op=skill[idx,5]; shiki=skill[175,17]; expected_shiki=css[132,17]; puts "operating_rules_block=#{op==expected_op ? "pass" : "fail"}"; puts "shiki_override_block=#{shiki==expected_shiki ? "pass" : "fail"}"'
sanctum/00 Inbox/harvest-encoding-2026-05-02.md:5:Encode harvest-frontend-phase-1-2026-05-02 by:
sanctum/01 Indexes/index.md:86:| `sanctum/00 Inbox/harvest-frontend-phase-1-2026-05-02.md` | [removed 2026-05-02] | 2026-05-02 |
```

Classification:
- `sanctum/00 Inbox/frontend-prose-route-skill-creation-2026-05-02.md:132` — HISTORICAL. Dated Inbox artifact; left unchanged.
- `sanctum/00 Inbox/harvest-encoding-2026-05-02.md:5` — HISTORICAL. Dated Inbox artifact; left unchanged.
- `sanctum/01 Indexes/index.md:86` — HISTORICAL. Removed-sentinel audit row retained intentionally per the promotion brief.

LIVE remediations applied before this verification pass:
- `bifrost/skills/frontend/frontend-prose-route/SKILL.md` — changed `sanctum/00 Inbox/harvest-frontend-phase-1-2026-05-02.md` to `sanctum/10 Knowledge/Concepts/harvest-frontend-phase-1.md`.
- `sanctum/01 Indexes/index.md` — replaced the stale active Inbox row state with the required removed sentinel and added the canonical Knowledge row.

```text
$ git -C sanctum diff --check
```

```text
$ git -C bifrost diff --check
```

```text
$ tail -n 1 'sanctum/01 Indexes/log.md'
## [2026-05-02] wiki/index-rebuild | [2 added, 2 modified, 1 removed] · session: phase-1-harvest-promotion
```

## deviations from the brief, if any

None.

## commit SHAs produced

- bifrost: `cb53e3de97c793c9704820ca5f3356cf10ac1b0a`
- sanctum: pending until the Sanctum repo commit in this dispatch
