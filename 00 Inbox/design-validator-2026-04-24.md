# design/validator — post-build visual inspection
Date: 2026-04-24
File: runestone/index.html
Finding: display headline overflow at wide viewport
Cause: clamp(32px, 6vw, 72px) on single-word uppercase
headline exceeded container width at >1100px viewport.
Builder missed this — mechanical CSS checks cannot
catch visual overflow.
Fix applied: clamp reduced to clamp(32px, 4vw, 64px),
overflow: hidden added to .header-left container.
Anti-pattern added to press.md and DESIGN_RUNESTONE.md.
Status: resolved
