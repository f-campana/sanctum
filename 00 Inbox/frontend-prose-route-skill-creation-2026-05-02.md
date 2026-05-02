# frontend-prose-route-skill-creation-2026-05-02

## dispatch summary

Create `bifrost/skills/frontend/frontend-prose-route/SKILL.md` from scratch using
the existing frontend skill template structure, the harvest proposal operating
rules, and the Press prose route implementation references; verify the new file,
run `wiki/index-rebuild` for the new skill and this run report, write this Inbox
run report, and produce separate `bifrost` and `sanctum` commits.

## actions taken

- `bifrost/skills/frontend/frontend-prose-route/SKILL.md` — `added`, `208` lines
  Frontmatter as written:
  ```yaml
  ---
  name: frontend/prose-route
  version: 1.0.0
  type: producer
  domain: frontend
  tier: action
  triggers:
    - /frontend-prose-route
    - "build a prose route"
    - "create a /spec route"
    - "render markdown into the product shell"
  reads_from: Design Contract (DESIGN_[PROJECT].md) + markdown source content + route specification
  writes_to: runestone/src/pages/[route]/[slug].astro + runestone/src/styles/[rune]-prose.css
  model_preference: claude-sonnet
  ---
  ```
  Sections written:
  - `When to use` — `15` lines
  - `What it does` — `26` lines
  - `What it does NOT do` — `17` lines
  - `Inputs` — `17` lines
  - `Output` — `11` lines
  - `Press rules the output must satisfy` — `22` lines
  - `Failure modes` — `23` lines
  - `Current implementation` — `50` lines
  - `Sources` — `9` lines
  Verbatim operating rules block:
  ```md
  Operating rules:
  - Do not rely on generic markdown defaults for headings, lists, tables, code, blockquotes, or inline code.
  - Create a dedicated prose stylesheet for the route and map every prose element to rune tokens.
  - If the markdown pipeline emits syntax-highlighted code, neutralise third-party token colours or disable them before delivery.
  - Report every framework default you had to override: markdown prose, syntax highlighting, list markers, table borders, and code backgrounds.
  ```
  Verbatim Shiki override block as cited:
  ```css
  /* Rule 5 — one structural colour.
     Override Shiki token colours to enforce
     Press Chromatism 2 near-monochrome. */
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

- `sanctum/01 Indexes/index.md` — `modified`
  Added `[pending description]` rows for:
  - `bifrost/skills/frontend/frontend-prose-route/SKILL.md`
  - `sanctum/00 Inbox/frontend-prose-route-skill-creation-2026-05-02.md`

- `sanctum/01 Indexes/log.md` — `modified`
  Appended:
  ```md
  ## [2026-05-02] wiki/index-rebuild | [2 added, 0 modified, 0 removed] · session: phase-1-frontend-prose-route-skill
  ```

- `sanctum/00 Inbox/frontend-prose-route-skill-creation-2026-05-02.md` — `added`
  This run report records the skill creation, verification commands, index
  update, and commit SHAs produced by the session.

## verification commands run with output

```text
$ test -d bifrost/skills/frontend/frontend-prose-route
$ echo $?
1
```

```text
$ find bifrost sanctum runestone -maxdepth 3 \( -name package.json -o -name pnpm-lock.yaml -o -name '.markdownlint*' -o -name '.prettierrc*' \) | sort
runestone/package.json
runestone/pnpm-lock.yaml
```

```text
$ ruby -e 'require "yaml"; path="bifrost/skills/frontend/frontend-prose-route/SKILL.md"; text=File.read(path); m=text.match(/\A---\n(.*?)\n---\n/m) or abort("frontmatter: missing"); data=YAML.safe_load(m[1], permitted_classes: [], aliases: false); required=%w[name version type domain tier triggers reads_from writes_to model_preference]; missing=required.reject { |k| data.key?(k) }; puts({frontmatter_open_close: "pass", required_fields: missing.empty? ? "pass" : "fail: #{missing.join(",")}", name: data["name"], version: data["version"], type: data["type"], domain: data["domain"], tier: data["tier"], triggers: data["triggers"].join(" | "), reads_from: data["reads_from"], writes_to: data["writes_to"], model_preference: data["model_preference"]}.map { |k,v| "#{k}=#{v}" }.join("\n"))'
frontmatter_open_close=pass
required_fields=pass
name=frontend/prose-route
version=1.0.0
type=producer
domain=frontend
tier=action
triggers=/frontend-prose-route | build a prose route | create a /spec route | render markdown into the product shell
reads_from=Design Contract (DESIGN_[PROJECT].md) + markdown source content + route specification
writes_to=runestone/src/pages/[route]/[slug].astro + runestone/src/styles/[rune]-prose.css
model_preference=claude-sonnet
```

```text
$ ruby -e 'path="bifrost/skills/frontend/frontend-prose-route/SKILL.md"; lines=File.readlines(path, chomp: true); headings=[]; lines.each_with_index { |line,i| headings << [line.sub(/^## /,""), i+1] if line.start_with?("## ") }; expected=["When to use","What it does","What it does NOT do","Inputs","Output","Press rules the output must satisfy","Failure modes","Current implementation","Sources"]; actual=headings.map { |h| h[0] }; puts "actual=#{actual.join(" | ")}"; puts "expected=#{expected.join(" | ")}"; puts "headings_match=#{actual==expected ? "pass" : "fail"}"; starts=headings.map { |h| h[1] } + [lines.length + 1]; headings.each_with_index { |(name,start), idx| count=starts[idx+1]-start; puts "section=#{name} lines=#{count}" }'
actual=When to use | What it does | What it does NOT do | Inputs | Output | Press rules the output must satisfy | Failure modes | Current implementation | Sources
expected=When to use | What it does | What it does NOT do | Inputs | Output | Press rules the output must satisfy | Failure modes | Current implementation | Sources
headings_match=pass
section=When to use lines=15
section=What it does lines=26
section=What it does NOT do lines=17
section=Inputs lines=17
section=Output lines=11
section=Press rules the output must satisfy lines=22
section=Failure modes lines=23
section=Current implementation lines=50
section=Sources lines=9
```

```text
$ ruby -e 'skill=File.readlines("bifrost/skills/frontend/frontend-prose-route/SKILL.md", chomp: true); harvest=File.readlines("sanctum/00 Inbox/harvest-frontend-phase-1-2026-05-02.md", chomp: true); css=File.readlines("runestone/src/styles/press-prose.css", chomp: true); expected_op=harvest[297,5]; idx=skill.index("Operating rules:"); op=skill[idx,5]; shiki=skill[175,17]; expected_shiki=css[132,17]; puts "operating_rules_block=#{op==expected_op ? "pass" : "fail"}"; puts "shiki_override_block=#{shiki==expected_shiki ? "pass" : "fail"}"'
operating_rules_block=pass
shiki_override_block=pass
```

`markdownlint-cli`, `prettier`, or equivalent repo-local Markdown tooling was not
present in `bifrost`, `sanctum`, or `runestone`, so task 4a was skipped after the
tooling search above.

## deviations from the brief, if any

- The brief listed `Current implementation` before `Failure modes`, but both
  `bifrost/skills/frontend/frontend-component/SKILL.md` and
  `bifrost/skills/frontend/frontend-island/SKILL.md` place `Failure modes`
  before `Current implementation`. I kept the canonical template order to avoid
  inventing a new structure.

## commit SHAs produced

- `bifrost` — `f2689a580dc0670960b53d844e1aa708095b0310`
- `sanctum` — indexes this report; SHA recorded in wiki log
