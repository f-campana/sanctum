# harvest-encoding-2026-05-02

## dispatch summary

Encode harvest-frontend-phase-1-2026-05-02 by:
- removing dead `.rune-content` CSS from `runestone/src/pages/runes/[slug].astro`
- adding four operating rules to `bifrost/CODEX.md`
- adding the single-source rule to `bifrost/skills/frontend/frontend-component/SKILL.md`
- appending the Shiki/rehype anti-pattern to `sanctum/10 Knowledge/Design/runes/press.md`
- running `wiki/index-rebuild` for the four named modified files with session label `phase-1-frontend-harvest-encoding`
- writing this Inbox run report

## actions taken

- `runestone/src/pages/runes/[slug].astro` — `0 added, 97 removed`
  Verbatim added text: none.
  Removed dead selectors only:
  - `.rune-content h2`
  - `.rune-content h3`
  - `.rune-content p`
  - `.rune-content pre`
  - `.rune-content code`
  - `.rune-content pre code`
  - `.rune-content table`
  - `.rune-content th`
  - `.rune-content td`
  - `.rune-content ul, .rune-content ol`
  - `.rune-content li`
  - `.rune-content li::before`
  - `.rune-content strong`

- `bifrost/CODEX.md` — `58 added, 0 removed`
  Verbatim added text:
  ```md
  **Route restructuring must enumerate removals in the
  same commit as the move.**
  When a dispatch moves content from one route to
  another, list:
  - every component or section that moves
  - every component or section that must be removed
    from the origin route
  - every CSS block, helper, or style selector that
    becomes dead after the move

  All removals — including dead style selectors — ship
  in the same commit as the move. Do not report a route
  split complete until the destination route renders the
  moved content, the origin route no longer renders it,
  and no dead styles for it remain in the tree.

  **Agent self-edits may not silently remove previously
  instructed code.**
  If you remove any code that was added earlier in the
  same dispatch chain, call it out explicitly before
  editing and again in the final report.
  Required report line:
  "Self-edit removal: [file] — removed [what] —
  reason [why]."
  If the removal changes behaviour on any viewport or
  input mode, name that behaviour explicitly.

  **Component moves require copy review in the same
  dispatch.**
  When a component moves between routes, review:
  - intro copy
  - captions
  - call-to-action labels
  - instructional notes

  Do not preserve route-specific framing by default.
  Re-check whether the moved copy still matches the new
  page purpose, audience, and interaction model.

  **Every dispatch that produces commits must write an
  Inbox run report.**
  The run report is the agent's account of what
  happened — distinct from commit messages, which
  describe intent, and from the dispatch brief, which
  describes intent before the fact.

  The report lives at sanctum/00 Inbox/[skill-or-task]-
  [target]-[date].md and contains:
  - dispatch summary (what was asked)
  - actions taken (file by file)
  - commands run with verbatim output for any
    verification step the dispatch named
  - deviations from the brief, if any
  - commit SHAs produced

  Commit messages may be cited as evidence of what
  changed. They may not stand in for the run report.
  ```

- `bifrost/skills/frontend/frontend-component/SKILL.md` — `9 added, 0 removed`
  Verbatim added text:
  ```md
  **Single source rule:**
  If a route needs a component that already exists,
  reuse the component file.
  Do not inline a second copy of the component markup
  into the route file to avoid modifying the original.
  If the route needs different copy or notes, add
  typed props or create a thin wrapper component and
  report the divergence explicitly.
  ```

- `sanctum/10 Knowledge/Design/runes/press.md` — `1 added, 0 removed`
  Verbatim added text:
  ```md
  - [ ] Syntax-highlighted markdown code blocks render with third-party theme colours or dark backgrounds → override Shiki/rehype code colours to `var(--pr-text)` and neutral Press surfaces before delivery
  ```

- `sanctum/01 Indexes/index.md` — `2 added, 2 removed`
  Verbatim added text:
  ```md
  | `bifrost/skills/frontend/frontend-component/SKILL.md` | Produces static Astro components from Design Contracts | 2026-05-02 |
  | `sanctum/10 Knowledge/Design/runes/press.md` | Defines Press Rune identity, tokens, motion, components | 2026-05-02 |
  ```

- `sanctum/01 Indexes/log.md` — `1 added, 0 removed`
  Verbatim added text:
  ```md
  ## [2026-05-02] wiki/index-rebuild | [0 added, 4 modified, 0 removed] · session: phase-1-frontend-harvest-encoding
  ```

## verification commands run with output

```text
$ grep -n 'rune-content' 'runestone/src/pages/runes/[slug].astro' || true
```

```text
$ pnpm build

> runestone@0.0.1 build /Users/fabiencampana/Documents/sanctum-bifrost/runestone
> astro build
15:23:20 [content] Syncing content
15:23:20 [content] Synced content
15:23:20 [types] Generated 262ms
15:23:20 [build] output: "static"
15:23:20 [build] mode: "static"
15:23:20 [build] directory: /Users/fabiencampana/Documents/sanctum-bifrost/runestone/dist/
15:23:20 [build] Collecting build info...
15:23:20 [build] ✓ Completed in 273ms.
15:23:20 [build] Building static entrypoints...
15:23:21 [vite] ✓ built in 756ms
15:23:21 [vite] ✓ built in 284ms
15:23:21 [build] Rearranging server assets...

 generating static routes 
15:23:21   ├─ /runes/press/spec/index.html (+18ms) 
15:23:21   ├─ /runes/press/index.html (+3ms) 
15:23:21   ├─ /index.html (+1ms) 
15:23:21 ✓ Completed in 69ms.

15:23:21 [build] ✓ Completed in 1.14s.
15:23:21 [build] 3 page(s) built in 1.42s
15:23:21 [build] Complete!
```

```text
$ pnpm dev --host 127.0.0.1

> runestone@0.0.1 dev /Users/fabiencampana/Documents/sanctum-bifrost/runestone
> astro dev --host 127.0.0.1

15:23:33 [types] Generated 0ms
15:23:33 [content] Syncing content
15:23:33 [content] Astro config changed
15:23:33 [content] Clearing content store
15:23:33 [content] Synced content
15:23:33 [vite] Re-optimizing dependencies because vite config has changed
 astro  v6.1.9 ready in 925 ms
┃ Local    http://127.0.0.1:4321/
15:23:33 watching for file changes...
```

```text
$ curl -s -o /dev/null -w '%{http_code}\n' http://127.0.0.1:4321/runes/press
200
```

```text
$ curl -s -o /dev/null -w '%{http_code}\n' http://127.0.0.1:4321/runes/press/spec
200
```

```text
$ rg -n '^\*\*Route restructuring must enumerate removals in the$|^\*\*Agent self-edits may not silently remove previously$|^\*\*Component moves require copy review in the same$|^\*\*Every dispatch that produces commits must write an$' bifrost/CODEX.md
148:**Route restructuring must enumerate removals in the
164:**Agent self-edits may not silently remove previously
175:**Component moves require copy review in the same
187:**Every dispatch that produces commits must write an
```

```text
$ git -C bifrost diff --check
```

```text
$ rg -n '^\*\*Single source rule:\*\*$' 'bifrost/skills/frontend/frontend-component/SKILL.md'
66:**Single source rule:**
```

```text
$ rg -n '^- \\[ \\] Syntax-highlighted markdown code blocks render with third-party theme colours or dark backgrounds → override Shiki/rehype code colours to `var\\(--pr-text\\)` and neutral Press surfaces before delivery$' 'sanctum/10 Knowledge/Design/runes/press.md'
484:- [ ] Syntax-highlighted markdown code blocks render with third-party theme colours or dark backgrounds → override Shiki/rehype code colours to `var(--pr-text)` and neutral Press surfaces before delivery
```

```text
$ tail -n 1 'sanctum/01 Indexes/log.md'
## [2026-05-02] wiki/index-rebuild | [0 added, 4 modified, 0 removed] · session: phase-1-frontend-harvest-encoding
```

## deviations from the brief, if any

None.

## commit SHAs produced

- `runestone` — `8785fc09697b94a7945e6c8f54900c15ba0403d9`
- `bifrost` — `0e72bbb4f00655f11efada6565ed3fecbf40fbe0`
- `sanctum` — pending until the sanctum commit that records this report exists
