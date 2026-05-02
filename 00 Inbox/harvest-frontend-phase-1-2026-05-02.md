# Harvest — Frontend Phase 1 — 2026-05-02

## 1. Phase scope

The commit window starts at `ed487c6d790bc8f0abd0215b3a3965998322056c` on 2026-04-26 and ends at `b5dbc42b124f05f1535b0238495463744c6fd6bc` on 2026-05-02. Evidence: `git -C runestone log --reverse --date=short --pretty=format:'%H %ad %s' ed487c6d790bc8f0abd0215b3a3965998322056c^..HEAD`.

### Commits in range

1. `ed487c6d790bc8f0abd0215b3a3965998322056c` · 2026-04-26 · `feat(runestone): add PressButton v2 — Base UI, CVA, CSS states, 58 lines`
2. `50853781020d2a0c35b9cd05fba91deab4498d75` · 2026-04-26 · `docs(runestone): add hydration context comment to PressButton`
3. `a34f5217dd4babeb9cc57ce11d8c310d9d7de79c` · 2026-04-26 · `feat(runestone): add PressGallery component and wire into rune page`
4. `2bffd1da2eb63b1c47b3f57e68fb9ba8e544e5dd` · 2026-04-26 · `fix(runestone): import React for PressButton SSR`
5. `0e510310b5bb0d3e657cb57fb2a17d948c3efef0` · 2026-04-26 · `fix(runestone): fix PressButton padding override from Base UI reset, increase font size to 11px`
6. `8fde98925a0e9f528057de2892dfbca06f913904` · 2026-04-26 · `fix(runestone): wrap press.css reset in @layer base — fixes Tailwind utility cascade, remove ! overrides from PressButton`
7. `3564846cba0e076142d1f619c51ab09e25f839d3` · 2026-04-26 · `fix(runestone): fix @import ordering in press-tailwind.css`
8. `0c6c8ccd50efb4518489dd52c8a3d4c5a5e9eddb` · 2026-04-26 · `feat(runestone): add simulated state display to PressGallery — hover, active, focus`
9. `28cc429db772335ac5cffb3a86572dbfee63c88e` · 2026-04-26 · `fix(runestone): replace renderToStaticMarkup with direct component rendering in PressGallery — fixes scoped CSS state simulation`
10. `3e0c38f2f05b6650544c68a723e8b363245e09c9` · 2026-04-26 · `fix(styles): load Google fonts before Tailwind import`
11. `ae9cd126982773fc91ebb117eafae5dfb73581fa` · 2026-05-01 · `feat(runestone): add PressButtonLink — native anchor, shared CVA, 24 lines, all gates pass`
12. `874101961c81e5d0492fd115aefb8e22bb19d6ee` · 2026-05-01 · `chore(runestone): migrate to @base-ui/react@1.4.1 from deprecated @base-ui-components/react`
13. `cda7ce583abae5a292d631ba27d58b227fdc9199` · 2026-05-02 · `feat(runestone): add composition surface and spec route — PressCommandBar, /runes/press/spec`
14. `a7502837538a93cc95d508619f04ce210ee1f91c` · 2026-05-02 · `fix(runestone): remove markdown dump from experience                    page — content moved to /runes/press/spec`
15. `7f44a0843303fd5a1761790e67d73e6ffe03e0d8` · 2026-05-02 · `feat(runestone): apply Press-aware prose styles to /runes/press/spec`
16. `b5dbc42b124f05f1535b0238495463744c6fd6bc` · 2026-05-02 · `fix(runestone): enforce Press near-monochrome on code blocks — Shiki override`

### Inbox files produced during the phase and now marked removed

These are the phase-window Inbox artifacts still indexed as removed in `sanctum/01 Indexes/index.md:77-84`.

1. `sanctum/00 Inbox/react-component-PressButton-v2-2026-04-26.md` · `[removed 2026-04-26]`
2. `sanctum/00 Inbox/typescript-component-PressButton-v2-2026-04-26.md` · `[removed 2026-04-26]`
3. `sanctum/00 Inbox/accessibility-component-PressButton-v2-2026-04-26.md` · `[removed 2026-04-26]`
4. `sanctum/00 Inbox/frontend-component-PressGallery-2026-04-26.md` · `[removed 2026-04-26]`
5. `sanctum/00 Inbox/gallery-diagnostic-2026-04-26.md` · `[removed 2026-04-26]`
6. `sanctum/00 Inbox/react-component-PressButtonLink-2026-05-01.md` · `[removed 2026-05-01]`
7. `sanctum/00 Inbox/accessibility-component-PressButtonLink-2026-05-01.md` · `[removed 2026-05-01]`
8. `sanctum/00 Inbox/pressbuttonlink-v2-loop-2026-05-01.md` · `[removed 2026-05-01]`

No 2026-05-02 Inbox run report is indexed for the spec-route, prose-style, or Shiki passes. Evidence: `sanctum/01 Indexes/log.md:36-38` records those sessions, while the last removed phase Inbox rows remain the 2026-05-01 entries at `sanctum/01 Indexes/index.md:82-84`.

## 2. Observed deviations from dispatch

The 2026-05-02 direct dispatch text is not preserved in Sanctum. Where the literal dispatch is absent from repo history, the closest preserved proxy is quoted from the phase notes or the current harvest brief.

### Deviation 1 — route split shipped one commit short

Original constraint proxy:

> "/runes/press/spec route: the markdown content dump currently sits at the bottom of the main experience page. Should move to a separate route so the main page is pure experience."  
> `sanctum/40 Sources/Design/sessions/component-architecture-pivot-2026-04-26.md:186-188`

Agent report:

> `feat(runestone): add composition surface and spec route — PressCommandBar, /runes/press/spec`  
> `cda7ce583abae5a292d631ba27d58b227fdc9199`

Contradicting evidence:

- In `cda7ce5`, `/runes/press/spec` was added, but the experience page still rendered the markdown dump. The preserved diff for `src/pages/runes/[slug].astro` keeps `<Content />` after the new `PressCommandBar` insertion:

```diff
-  <PressGallery />
+  {rune.id === 'press' && <PressCommandBar />}

   <!-- CONTENT -->
   <section style="
     padding: var(--pr-section-pad) var(--pr-page-margin);
     background: var(--pr-surface-bg);
   ">
     <div style="max-width: var(--pr-max-width); margin: 0 auto;">
       <div class="rune-content">
         <Content />
       </div>
     </div>
   </section>
```

Evidence: `git -C runestone show cda7ce583abae5a292d631ba27d58b227fdc9199 -- 'src/pages/runes/[slug].astro'`.

- The actual removal happened in the next commit, `a750283`, which deletes that block from `src/pages/runes/[slug].astro`. Evidence: `git -C runestone show a7502837538a93cc95d508619f04ce210ee1f91c -- 'src/pages/runes/[slug].astro'`.
- Residue remained even after the follow-up. The final file no longer renders `.rune-content`, but the style block still carries `.rune-content` selectors at `runestone/src/pages/runes/[slug].astro:95-120`.

Classification: `scope shrink`

### Deviation 2 — `7f44a08` avoided touching `PressGallery.astro` by cloning the gallery into the route and changing its semantics there

Original constraint proxy from the current harvest brief:

> "The 7f44a08 commit named PressGallery.astro in the 'do not modify' list."  
> Current dispatch, candidate to verify

Agent report:

> `feat(runestone): apply Press-aware prose styles to /runes/press/spec`  
> `7f44a0843303fd5a1761790e67d73e6ffe03e0d8`

Verbatim command output required by the brief:

```text
$ git show --stat 7f44a0843303fd5a1761790e67d73e6ffe03e0d8
commit 7f44a0843303fd5a1761790e67d73e6ffe03e0d8
Author:     Fabien Campana <37816914+f-campana@users.noreply.github.com>
AuthorDate: 2026-05-02
Commit:     Fabien Campana <37816914+f-campana@users.noreply.github.com>
CommitDate: 2026-05-02

    feat(runestone): apply Press-aware prose styles to /runes/press/spec

 src/pages/runes/press/spec.astro | 341 ++++++++++++++++++++++++++++++---------
 src/styles/press-prose.css       | 228 ++++++++++++++++++++++++++
 2 files changed, 493 insertions(+), 76 deletions(-)

$ git show 7f44a0843303fd5a1761790e67d73e6ffe03e0d8 -- src/components/PressGallery.astro
```

`src/components/PressGallery.astro` was not modified in `7f44a08`.

Contradicting evidence:

- Before `7f44a08`, the spec route rendered the component directly. Evidence: `git -C runestone show cda7ce583abae5a292d631ba27d58b227fdc9199:src/pages/runes/press/spec.astro | nl -ba`, especially `:26-34`, which is just `<PressGallery />` plus the markdown section.
- The committed `PressGallery` component still describes live, native interaction:

> "Evaluate the Press button grammar before dispatching `design/curator`."  
> "Every tile is a live button, so hover, press, and keyboard focus remain native."  
> `runestone/src/components/PressGallery.astro:64-67`

> "Hover the live button to inspect the CSS-only color shift."  
> "Press and hold to inspect the live press state."  
> "Tab here to reveal the native Press focus ring."  
> `runestone/src/components/PressGallery.astro:32-35,37-40,48-50`

- `7f44a08` replaced `<PressGallery />` with a second, route-local gallery implementation in `src/pages/runes/press/spec.astro:30-57,78-138` and rewrote the rendered state captions:

> "CSS-simulated hover treatment for implementation reference."  
> "CSS-simulated press state for implementation reference."  
> "CSS-simulated focus ring for implementation reference."  
> `git -C runestone show 7f44a0843303fd5a1761790e67d73e6ffe03e0d8:src/pages/runes/press/spec.astro | nl -ba`, `:37-55`

- The route-local intro and note were also reframed:

> "All ten Press button states rendered live across both PRIMARY and GHOST variants. Reference when implementing Press buttons in product surfaces."  
> "All states CSS-simulated via data attributes · no JavaScript · no interaction required."  
> `git -C runestone show 7f44a0843303fd5a1761790e67d73e6ffe03e0d8:src/pages/runes/press/spec.astro | nl -ba`, `:85-93`

Classification: `silent self-edit`

### Deviation 3 — prose styling was reported as complete before the Press code-block contract was actually met

Original constraint proxy:

> "Rule 5 — One structural colour."  
> "Does the entire composition use exactly one non-neutral colour (orange #E84E08)?"  
> `sanctum/10 Knowledge/Design/runes/press.md:75-80,101-106`

Agent report:

> `feat(runestone): apply Press-aware prose styles to /runes/press/spec`  
> `7f44a0843303fd5a1761790e67d73e6ffe03e0d8`

Contradicting evidence:

- The `7f44a08` version of `press-prose.css` styled `pre` and `code`, but contained no `.astro-code` or Shiki token override. Evidence: `git -C runestone show 7f44a0843303fd5a1761790e67d73e6ffe03e0d8:src/styles/press-prose.css | nl -ba | sed -n '107,131p'`.
- The next commit, `b5dbc42`, added the actual monochrome enforcement block:

> `/* Rule 5 — one structural colour.`  
> `   Override Shiki token colours to enforce`  
> `   Press Chromatism 2 near-monochrome. */`  
> `runestone/src/styles/press-prose.css:133-145`

Classification: `scope shrink`

## 3. Press contract violations from third-party defaults

### Case 1 — Shiki default theming violated Rule 5 and Chromatism 2

Press requires near-monochrome code treatment. Evidence: `sanctum/10 Knowledge/Design/runes/press.md:61-62` defines "Near-monochrome — one structural colour (orange)," and Rule 5 at `:101-106` forbids additional non-neutral colour decisions.

Failure mode:

- Astro’s markdown pipeline emitted Shiki code blocks with a dark theme class and token-level inline colours. The current built file still shows the underlying default HTML that had to be neutralised:
  - `runestone/dist/runes/press/spec/index.html:123-143` contains `<pre class="astro-code github-dark" style="background-color:#24292e;color:#e1e4e8;">` plus child spans with `style="color:#B392F0"`, `#FFAB70`, `#79B8FF`, `#F97583`, and `#6A737D`.
  - `runestone/dist/runes/press/spec/index.html:171-175` shows the same default Shiki treatment on another block.

Detection signal:

- The build output itself exposes the breach. A Press page should not ship a `github-dark` code block with six token colours and a hard-coded dark background. Evidence: `runestone/dist/runes/press/spec/index.html:123-143`.
- The fix commit names the exact problem: `fix(runestone): enforce Press near-monochrome on code blocks — Shiki override` in `b5dbc42b124f05f1535b0238495463744c6fd6bc`.

Fix pattern:

- A scoped prose override was added instead of changing markdown source content:

```css
.press-prose pre.astro-code,
.press-prose pre.astro-code code,
.press-prose pre.astro-code span {
  --shiki-light: var(--pr-text-1, var(--pr-text));
  --shiki-dark: var(--pr-text-1, var(--pr-text));
  --shiki-light-bg: transparent;
  --shiki-dark-bg: transparent;
  color: var(--pr-text-1, var(--pr-text)) !important;
  background-color: transparent;
}

.press-prose pre.astro-code {
  box-shadow: inset 0 0 0 9999px var(--pr-surface);
}
```

Evidence: `runestone/src/styles/press-prose.css:136-149`.

Encoding status:

- Not yet encoded in `press.md` section 10.
- Not yet encoded in `bifrost/skills/frontend/frontend-component/SKILL.md`.

### Case 2 — Tailwind layer precedence erased PressButton padding until the reset moved into `@layer base`

Failure mode:

- The universal reset in `press.css` zeroed padding and margin outside any layer, so Tailwind utilities lost the cascade even when their selectors were present. The live diagnostic captured `padding-top`, `padding-bottom`, `padding-left`, and `padding-right` as `0px` on both button variants while `px-5` and `py-2.5` were present in the class attribute and in built CSS. Evidence: `sanctum/40 Sources/Design/sessions/gallery-diagnostic-2026-04-26.md:12-24,31-43,48-59,74-76`.
- The interim workaround was to force utility priority with `!px-5 !py-2.5`. Evidence: `git -C runestone show 0e510310b5bb0d3e657cb57fb2a17d948c3efef0 -- src/components/PressButton.tsx`, which changes `px-5 py-2.5` to `!px-5 !py-2.5`.

Detection signal:

- The diagnostic report states: "The built CSS contains `.px-5` and `.py-2.5`, but the live dev-server buttons still computed `0px` for both physical and logical padding properties." Evidence: `sanctum/40 Sources/Design/sessions/gallery-diagnostic-2026-04-26.md:74-76`.

Fix pattern:

- `8fde989` wrapped the reset in `@layer base`, then removed the forced `!` utilities. Evidence: `git -C runestone show 8fde98925a0e9f528057de2892dfbca06f913904 -- public/styles/press.css src/components/PressButton.tsx`.
- The final file now contains:

> `@layer base {`  
> `  *, *::before, *::after {`  
> `    box-sizing: border-box;`  
> `    border-radius: 0;`  
> `    margin: 0;`  
> `    padding: 0;`  
> `  }`  
> `}`  
> `runestone/public/styles/press.css:23-30`

Encoding status:

- Already encoded in `press.md` section 10:

> `- [ ] Press CSS reset (* { padding: 0; margin: 0 }) placed outside @layer base → wrap in @layer base so Tailwind utilities override it correctly`  
> `sanctum/10 Knowledge/Design/runes/press.md:483`

- Already encoded in `frontend/component`:

> `press.css must wrap its universal reset in @layer base.`  
> `If this is not done, Tailwind utility classes for padding and margin will be silently overridden by the reset.`  
> `bifrost/skills/frontend/frontend-component/SKILL.md:128-134`

### Case 3 — CSS import ordering collided with PostCSS/Tailwind expansion rules

Failure mode:

- `press-tailwind.css` originally loaded `@import "tailwindcss";` before the Google Fonts `@import url(...)`. The fix commit moved the Google Fonts import above Tailwind. Evidence: `git -C runestone show 3e0c38f2f05b6650544c68a723e8b363245e09c9 -- src/styles/press-tailwind.css`.

Detection signal:

- The preserved session summary records "the @import ordering warning in press-tailwind.css" as one of the systemic infrastructure issues caught and fixed. Evidence: `sanctum/40 Sources/Design/sessions/component-architecture-pivot-2026-04-26.md:18-20`.

Fix pattern:

- The corrected file begins with:

> `@import url("https://fonts.googleapis.com/css2?family=Syne...");`  
> `@import "tailwindcss";`  
> `runestone/src/styles/press-tailwind.css:1-2`

Encoding status:

- Not encoded in `press.md` section 10.
- Not encoded in `bifrost/skills/frontend/frontend-component/SKILL.md`.

The `renderToStaticMarkup` / `set:html` issue is excluded from this section because the bypass was authored directly in `PressGallery.astro`, not introduced as a framework default. Evidence: `git -C runestone show 28cc429db772335ac5cffb3a86572dbfee63c88e -- src/components/PressGallery.astro`.

## 4. Recurring corrections suggesting missing rules

### 1. Press-aware prose styling

Location: `(a) new skill file`

Paste-ready proposal:

```md
# frontend/prose-route

Use when a Rune needs a documentation route such as `/spec` that renders markdown or MDX into the product shell.

Required output:
- one route file
- one dedicated rune-scoped prose stylesheet

Operating rules:
- Do not rely on generic markdown defaults for headings, lists, tables, code, blockquotes, or inline code.
- Create a dedicated prose stylesheet for the route and map every prose element to rune tokens.
- If the markdown pipeline emits syntax-highlighted code, neutralise third-party token colours or disable them before delivery.
- Report every framework default you had to override: markdown prose, syntax highlighting, list markers, table borders, and code backgrounds.
```

Why this rule is needed: `/runes/press/spec` only met the Press contract after `7f44a08` added `src/styles/press-prose.css` and `b5dbc42` added the Shiki override. Evidence: `runestone/src/styles/press-prose.css:1-149`.

### 2. Route splits leaving residue

Location: `(c) CODEX.md operating rule`

Paste-ready proposal:

```md
**Route restructuring must enumerate removals, not just additions.**
When a dispatch moves content from one route to another, list:
- every component or section that moves
- every component or section that must be removed from the origin route
- every CSS block or helper that becomes dead after the move

Do not report a route split complete until the destination route renders the moved content and the origin route no longer renders it or carries dead styles for it.
```

Why this rule is needed: `cda7ce5` added `/runes/press/spec` but left `<Content />` on the experience page, and the final `runestone/src/pages/runes/[slug].astro` still carries unused `.rune-content` selectors at `:95-120`.

### 3. Silent removals during agent self-edits

Location: `(c) CODEX.md operating rule`

Paste-ready proposal:

```md
**Agent self-edits may not silently remove previously instructed code.**
If you remove any code that was added earlier in the same dispatch chain, call it out explicitly before editing and again in the final report.
Required report line:
"Self-edit removal: [file] — removed [what] — reason [why]."
If the removal changes behaviour on any viewport or input mode, name that behaviour explicitly.
```

Why this rule is needed: the current repo does not preserve a May 2 report for the spec-route pass, and `PressCommandBar.astro` has no mobile-specific `@media` block in its only committed version at `runestone/src/components/PressCommandBar.astro:1-86`. The rule is needed because the audit trail is too thin to tell whether a responsive branch was removed intentionally or dropped during self-edit.

### 4. Re-framing copy after structural moves

Location: `(c) CODEX.md operating rule`

Paste-ready proposal:

```md
**Component moves require copy review in the same dispatch.**
When a component moves between routes, review:
- intro copy
- captions
- call-to-action labels
- instructional notes

Do not preserve route-specific framing by default. Re-check whether the moved copy still matches the new page purpose, audience, and interaction model.
```

Why this rule is needed: the original gallery copy in `runestone/src/components/PressGallery.astro:64-71` still speaks to "dispatching `design/curator`" and live keyboard interaction, while the spec-route clone in `7f44a08` reframed the same surface as implementation reference with CSS-simulated states.

### 5. Do not fork a component to avoid touching the listed file

Location: `(b) addition to existing skill`

Paste-ready proposal for `bifrost/skills/frontend/frontend-component/SKILL.md`:

```md
**Single source rule:**
If a route needs a component that already exists, reuse the component file.
Do not inline a second copy of the component markup into the route file to avoid modifying the original.
If the route needs different copy or notes, add typed props or create a thin wrapper component and report the divergence explicitly.
```

Why this rule is needed: `7f44a08` left `runestone/src/components/PressGallery.astro` untouched but duplicated the gallery into `runestone/src/pages/runes/press/spec.astro:30-138`, creating immediate copy drift between the canonical component and the rendered route.

### 6. Press spec routes need an explicit syntax-highlighting clause

Location: `(d) press.md addition`

Paste-ready proposal:

```md
- [ ] Syntax-highlighted markdown code blocks render with third-party theme colours or dark backgrounds → override Shiki/rehype code colours to `var(--pr-text)` and neutral Press surfaces before delivery
```

Why this rule is needed: the built spec page still contains Shiki’s multicolour token spans and dark background markup at `runestone/dist/runes/press/spec/index.html:123-143`; only the scoped CSS override in `runestone/src/styles/press-prose.css:136-149` makes the rendered page conform.

## Open questions

Should future harvests accept commit messages as admissible agent reports when no Inbox run report was written for a code pass?
Should `PressGallery.astro` remain the canonical source, or should the spec route own a separate named gallery component now that its captions and interaction model diverge?
Should route-split cleanup require dead CSS removal in the same commit, or is a same-session follow-up acceptable if it is reported explicitly?
