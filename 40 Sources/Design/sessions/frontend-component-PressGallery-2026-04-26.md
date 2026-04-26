# frontend/component — PressGallery — 2026-04-26

Component type chosen: `.astro`

Why:
The gallery does not need runtime state, event handlers, or hydration. Hover,
active, disabled, and keyboard focus are all native button states already
provided by `PressButton`, so a static Astro component is sufficient. The
component imports `PressButton` and server-renders it into static HTML so the
result stays interactive without becoming an island.

Output:
- Component: `runestone/src/components/PressGallery.astro`
- Props: none
- Line count: 310

Press inviolable rule checks:
- Rule 1 — Orange is structural, never decorative: pass
- Rule 2 — Zero radius, everywhere: pass
- Rule 3 — 2px borders throughout: pass
- Rule 4 — Light-first, always: pass
- Rule 5 — One structural colour: pass
- Rule 6 — Semantic aliases are binding: pass
