# Index

## Core
- [System Spec](../system-spec.md)
- [Design Press Rune](../10%20Knowledge/Design/runes/press.md)
- [Routing Guide](../10%20Knowledge/Design/routing-guide.md)
- [Design Principles](../10%20Knowledge/Design/design-principles.md)

## Sources
- [Design Session Summary](../../40%20Sources/Design/sessions/design-pipeline-session-2026-04-22.md)

## Notes
- Phase 0 only.
- Sanctum is the compiled wiki, not the schema layer.

## Sanctum

| File | Description | Updated |
|---|---|---|
| `sanctum/.gitignore` | [pending description] | 2026-04-24 |

## Bifrost

| File | Description | Updated |
|---|---|---|
| `bifrost/CODEX.md` | Defines system operating rules and canonical boot context | 2026-05-02 |
| `bifrost/skills/frontend/frontend-component/SKILL.md` | Produces static Astro components from Design Contracts | 2026-04-26 |
| `bifrost/skills/frontend/frontend-island/SKILL.md` | Produces hydrated React islands for Press interactions | 2026-04-24 |
| `bifrost/skills/github/github-read-file/SKILL.md` | Reports exact on-disk file content to Inbox | 2026-04-23 |
| `bifrost/skills/github/github-read-diff/SKILL.md` | Reports structured git diffs for one repository | 2026-04-23 |
| `bifrost/skills/typescript/typescript-component/SKILL.md` | Validates TypeScript safety for Press component code | 2026-04-25 |
| `bifrost/skills/react/react-component/SKILL.md` | Produces Base UI React components using CVA variants | 2026-05-01 |
| `bifrost/skills/accessibility/accessibility-component/SKILL.md` | Validates interactive component accessibility and Base UI integration | 2026-05-01 |
| `bifrost/skills/wiki/wiki-index-rebuild/SKILL.md` | Updates indexed changed files and appends session log | 2026-04-23 |

## Runestone

| File | Description | Updated |
|---|---|---|
| `runestone/DESIGN_RUNESTONE.md` | Defines Press-instanced design contract for Runestone | 2026-04-25 |
| `runestone/index.html` | [removed 2026-04-24] | 2026-04-24 |
| `runestone/package.json` | Configures Astro, React, Tailwind, Base UI dependencies | 2026-05-01 |
| `runestone/tsconfig.json` | Enforces strict TypeScript and source path aliasing | 2026-04-26 |
| `runestone/.gitignore` | Excludes builds, diagnostics, dependencies, logs, editor files | 2026-04-26 |
| `runestone/README.md` | Introduces Runestone commands and design contract location | 2026-04-24 |
| `runestone/src/content.config.ts` | Defines Astro content schema for Rune markdown | 2026-04-24 |
| `runestone/src/components/RadarRow.astro` | Renders one scored Rune radar axis row | 2026-04-24 |
| `runestone/src/components/RuneHero.astro` | Renders Rune identity hero and metadata panel | 2026-04-24 |
| `runestone/src/components/PressLayout.astro` | Provides Press shell, fonts, styles, and navigation | 2026-04-25 |
| `runestone/astro.config.mjs` | Configures Astro React integration, Tailwind, and aliases | 2026-04-26 |
| `runestone/src/pages/runes/[slug].astro` | Builds static Rune pages with radar, gallery, content | 2026-04-26 |
| `runestone/src/styles/press-tailwind.css` | Maps Press tokens into Tailwind theme aliases | 2026-04-25 |
| `runestone/src/components/PressButton.tsx` | Implements Press button primitive with CVA variants | 2026-05-01 |
| `runestone/src/components/PressButtonLink.tsx` | Implements link variant sharing Press button styles | 2026-05-01 |
| `runestone/src/lib/utils.ts` | Merges clsx class values through tailwind-merge | 2026-04-26 |
| `runestone/src/components/PressGallery.astro` | Displays live Press button variants and states | 2026-04-26 |

## 00 Inbox

| File | Description | Updated |
|---|---|---|
| `sanctum/00 Inbox/github-read-file-2026-04-23.md` | [removed 2026-04-23] | 2026-04-23 |
| `sanctum/00 Inbox/github-read-diff-2026-04-23.md` | [removed 2026-04-23] | 2026-04-23 |
| `sanctum/00 Inbox/github-read-diff-2026-04-23-b.md` | [removed 2026-04-23] | 2026-04-23 |
| `sanctum/00 Inbox/design-validator-2026-04-24.md` | [removed 2026-04-24] | 2026-04-24 |
| `sanctum/00 Inbox/design-builder-2026-04-24.md` | [removed 2026-04-24] | 2026-04-24 |
| `sanctum/00 Inbox/design-curator-2026-04-23.md` | [removed 2026-04-24] | 2026-04-24 |
| `sanctum/00 Inbox/frontend-component-RadarRow-2026-04-24.md` | [removed 2026-04-24] | 2026-04-24 |
| `sanctum/00 Inbox/frontend-component-RuneHero-2026-04-24.md` | [removed 2026-04-24] | 2026-04-24 |
| `sanctum/00 Inbox/press-tailwind-adapter-report-2026-04-25.md` | [removed 2026-04-25] | 2026-04-25 |
| `sanctum/00 Inbox/react-component-PressButton-2026-04-25.md` | [removed 2026-04-26] | 2026-04-26 |
| `sanctum/00 Inbox/typescript-component-PressButton-2026-04-25.md` | [removed 2026-04-26] | 2026-04-26 |
| `sanctum/00 Inbox/accessibility-component-PressButton-2026-04-25.md` | [removed 2026-04-26] | 2026-04-26 |
| `sanctum/00 Inbox/react-component-PressButton-v2-2026-04-26.md` | [removed 2026-04-26] | 2026-04-26 |
| `sanctum/00 Inbox/typescript-component-PressButton-v2-2026-04-26.md` | [removed 2026-04-26] | 2026-04-26 |
| `sanctum/00 Inbox/accessibility-component-PressButton-v2-2026-04-26.md` | [removed 2026-04-26] | 2026-04-26 |
| `sanctum/00 Inbox/frontend-component-PressGallery-2026-04-26.md` | [removed 2026-04-26] | 2026-04-26 |
| `sanctum/00 Inbox/gallery-diagnostic-2026-04-26.md` | [removed 2026-04-26] | 2026-04-26 |
| `sanctum/00 Inbox/react-component-PressButtonLink-2026-05-01.md` | [removed 2026-05-01] | 2026-05-01 |
| `sanctum/00 Inbox/accessibility-component-PressButtonLink-2026-05-01.md` | [removed 2026-05-01] | 2026-05-01 |
| `sanctum/00 Inbox/pressbuttonlink-v2-loop-2026-05-01.md` | [removed 2026-05-01] | 2026-05-01 |

## 10 Knowledge

| File | Description | Updated |
|---|---|---|
| `sanctum/10 Knowledge/Concepts/press-component-architecture-adr.md` | Defines Press component architecture decisions and evidence | 2026-05-01 |
| `sanctum/10 Knowledge/Concepts/system-glossary.md` | Defines canonical system vocabulary and naming rules | 2026-04-23 |
| `sanctum/10 Knowledge/Design/runes/press.md` | Defines Press Rune identity, tokens, motion, components | 2026-04-25 |

## 40 Sources

| File | Description | Updated |
|---|---|---|
| `sanctum/40 Sources/Design/sessions/build-correction-session-2026-04-23.md` | [removed 2026-04-24] | 2026-04-24 |
| `sanctum/40 Sources/Design/sessions/phase-0-1-implementation-loop-2026-04-24.md` | Summarizes Phase 0 correction loop and Runestone sequencing | 2026-04-24 |
| `sanctum/40 Sources/Design/sessions/design-curator-run-2026-04-23.md` | Records Runestone Design Contract instancing outputs and phrases | 2026-04-24 |
| `sanctum/40 Sources/Design/sessions/design-builder-run-2026-04-24.md` | Records Runestone static build results and rule checks | 2026-04-24 |
| `sanctum/40 Sources/Design/sessions/design-validator-run-2026-04-24.md` | Documents Runestone headline overflow finding and fix | 2026-04-24 |
| `sanctum/40 Sources/Design/sessions/runestone-static-proof-2026-04-24.html` | Contains standalone Press-styled Runestone static HTML proof | 2026-04-24 |
| `sanctum/40 Sources/Design/sessions/frontend-component-RadarRow-2026-04-24.md` | Reports RadarRow component output, props, and Press checks | 2026-04-24 |
| `sanctum/40 Sources/Design/sessions/frontend-component-RuneHero-2026-04-24.md` | Reports RuneHero component output, props, and Press checks | 2026-04-24 |
| `sanctum/40 Sources/Design/sessions/press-tailwind-adapter-report-2026-04-25.md` | Maps Press tokens to Tailwind semantic slots | 2026-04-25 |
| `sanctum/40 Sources/Design/sessions/react-component-PressButton-2026-04-25.md` | Documents superseded React Aria PressButton implementation | 2026-04-26 |
| `sanctum/40 Sources/Design/sessions/typescript-component-PressButton-2026-04-25.md` | Validates superseded PressButton TypeScript corrections | 2026-04-26 |
| `sanctum/40 Sources/Design/sessions/accessibility-component-PressButton-2026-04-25.md` | Validates superseded PressButton accessibility behavior | 2026-04-26 |
| `sanctum/40 Sources/Design/sessions/react-component-PressButton-v2-2026-04-26.md` | Documents Base UI PressButton implementation and supporting changes | 2026-04-26 |
| `sanctum/40 Sources/Design/sessions/typescript-component-PressButton-v2-2026-04-26.md` | Validates PressButton v2 TypeScript fixes and config | 2026-04-26 |
| `sanctum/40 Sources/Design/sessions/accessibility-component-PressButton-v2-2026-04-26.md` | Validates PressButton v2 accessibility and runtime test needs | 2026-04-26 |
| `sanctum/40 Sources/Design/sessions/frontend-component-PressGallery-2026-04-26.md` | Reports static PressGallery component and Press checks | 2026-04-26 |
| `sanctum/40 Sources/Design/sessions/gallery-diagnostic-2026-04-26.md` | Captures PressGallery computed styles and Tailwind utility diagnostics | 2026-04-26 |
| `sanctum/40 Sources/Design/sessions/react-component-PressButtonLink-2026-05-01.md` | Documents native anchor PressButtonLink implementation | 2026-05-01 |
| `sanctum/40 Sources/Design/sessions/accessibility-component-PressButtonLink-2026-05-01.md` | Validates PressButtonLink native link accessibility | 2026-05-01 |
| `sanctum/40 Sources/Design/sessions/pressbuttonlink-v2-loop-2026-05-01.md` | Records PressButtonLink loop failure, fixes, and pass status | 2026-05-01 |
| `sanctum/40 Sources/Design/sessions/component-architecture-pivot-2026-04-26.md` | [pending description] | 2026-05-02 |
| `sanctum/40 Sources/React/Concepts/React - Component Model, Props, and State.md` | Explains React props, state ownership, and component identity | 2026-04-25 |
| `sanctum/40 Sources/React/Concepts/React - Composition, Lifting State, and Controlled vs Uncontrolled.md` | Explains React composition, lifted state, and controlled APIs | 2026-04-25 |
| `sanctum/40 Sources/React/Concepts/React - Concurrent React, Suspense, and Transitions.md` | Explains concurrent scheduling, Suspense boundaries, and transitions | 2026-04-25 |
| `sanctum/40 Sources/React/Concepts/React - Hooks, Effects, and Closures.md` | Explains hooks, effects, refs, and closure snapshots | 2026-04-25 |
| `sanctum/40 Sources/React/Concepts/React - Memoization and Performance Tradeoffs.md` | Explains memoization limits and structural performance fixes | 2026-04-25 |
| `sanctum/40 Sources/React/Concepts/React - Reconciliation, Keys, and Fiber.md` | Explains reconciliation identity, keys, and Fiber bookkeeping | 2026-04-25 |
| `sanctum/40 Sources/React/Concepts/React - Rendering and Re-rendering.md` | Explains render, commit, and re-render causes | 2026-04-25 |
| `sanctum/40 Sources/React/Concepts/React - Server Components and Internals.md` | Explains Server Components, Fiber internals, and schedulers | 2026-04-25 |
| `sanctum/40 Sources/React/Lessons/React - Lesson 01 - Foundations - Hooks, Composition, State, and Performance Basics.md` | Teaches hooks, composition, state, and performance basics | 2026-04-25 |
| `sanctum/40 Sources/React/Lessons/React - Lesson 02 - Rendering, Closures, and Re-rendering.md` | Teaches render snapshots, stale closures, and re-render causes | 2026-04-25 |
| `sanctum/40 Sources/React/Lessons/React - Lesson 03 - Reconciliation, Keys, and Fiber.md` | Teaches reconciliation identity, keys, and Fiber | 2026-04-25 |
| `sanctum/40 Sources/React/Lessons/React - Lesson 04 - Advanced Patterns at Scale.md` | Teaches scalable composition, state ownership, and patterns | 2026-04-25 |
| `sanctum/40 Sources/React/Lessons/React - Lesson 05 - Performance Beyond Memo.md` | Teaches structural performance before memoization | 2026-04-25 |
| `sanctum/40 Sources/React/Lessons/React - Lesson 06 - Concurrent React, Suspense, and Transitions.md` | Teaches transitions, Suspense, scheduling, and streaming | 2026-04-25 |
| `sanctum/40 Sources/React/Lessons/React - Lesson 07 - Server Components and React Internals.md` | Teaches Server Components boundaries and React internals | 2026-04-25 |
| `sanctum/40 Sources/React/react-map.md` | Organizes React lessons, concepts, exercises, and path | 2026-04-25 |
| `sanctum/40 Sources/TypeScript/Concepts/TypeScript - Compiler and API Design.md` | Explains compiler pipeline, inference-friendly APIs, and type costs | 2026-04-25 |
| `sanctum/40 Sources/TypeScript/Concepts/TypeScript - Narrowing, Discriminated Unions, and Exhaustiveness.md` | Explains narrowing, discriminated unions, and exhaustive checks | 2026-04-25 |
| `sanctum/40 Sources/TypeScript/Concepts/TypeScript - Runtime Boundaries and Safety.md` | Explains runtime validation, branded types, and unsafe boundaries | 2026-04-25 |
| `sanctum/40 Sources/TypeScript/Concepts/TypeScript - Type System Fundamentals.md` | Explains erasure, structural typing, unions, and generics | 2026-04-25 |
| `sanctum/40 Sources/TypeScript/Concepts/TypeScript - Type-Level Programming.md` | Explains conditional types, infer, mapped types, and variance | 2026-04-25 |
| `sanctum/40 Sources/TypeScript/Lessons/TypeScript - Lesson 01 - Foundations - Erasure, Structural Typing, and Narrowing.md` | Teaches erasure, structural typing, narrowing, and unions | 2026-04-25 |
| `sanctum/40 Sources/TypeScript/Lessons/TypeScript - Lesson 02 - Generics, keyof, and Utility Types.md` | Teaches generics, keyof, indexed access, and utilities | 2026-04-25 |
| `sanctum/40 Sources/TypeScript/Lessons/TypeScript - Lesson 03 - Advanced Type Programming - Conditional Types, infer, Variance, and Template Literals.md` | Teaches conditional types, infer, variance, and templates | 2026-04-25 |
| `sanctum/40 Sources/TypeScript/Lessons/TypeScript - Lesson 04 - Staff and Principal - Branding, Validation, Compiler Boundaries, and API Design.md` | Teaches branding, validation, compiler boundaries, and API design | 2026-04-25 |
| `sanctum/40 Sources/TypeScript/typescript-map.md` | Organizes TypeScript lessons, concepts, exercises, and path | 2026-04-25 |
| `sanctum/40 Sources/Accessibility/wai-aria-authoring-practices-guide.md` | Summarizes APG widget roles, keyboard models, and focus management | 2026-04-25 |
| `sanctum/40 Sources/Accessibility/adobe-react-aria-styling.md` | Summarizes React Aria state exposure and styling boundaries | 2026-04-25 |

## 99 Templates

| File | Description | Updated |
|---|---|---|
| `sanctum/99 Templates/SKILL.md` | Defines standard skill metadata, scope, inputs, outputs | 2026-04-23 |
| `sanctum/99 Templates/rune.md` | Defines Rune structure, tokens, motion, routing sections | 2026-04-23 |
| `sanctum/99 Templates/session-summary.md` | Defines session summary decisions, artifacts, validation format | 2026-04-23 |
| `sanctum/99 Templates/concept-note.md` | Defines concept note summary, properties, system usage | 2026-04-23 |
| `sanctum/99 Templates/source-note.md` | Defines source capture summary, relevance, derivation format | 2026-04-23 |
| `sanctum/99 Templates/memory-note.md` | Defines memory note verified facts, inferences, constraints | 2026-04-23 |
