# Gallery Diagnostic — 2026-04-26

## Scope

- Target URL: `http://localhost:4321/runes/press`
- Section inspected: `PressGallery`
- Desktop screenshot: `runestone/scripts/gallery-diagnostic-desktop.png`
- Mobile screenshot: `runestone/scripts/gallery-diagnostic-mobile.png`

## Primary Variant · First Button · DEFAULT State

Class attribute: `border-2 border-solid rounded-none shadow-none inline-flex items-center justify-center gap-2 px-5 py-2.5 font-mono text-[9px] font-medium uppercase tracking-[0.1em] transition-[background-color,border-color,color,transform] duration-120 ease-linear cursor-pointer enabled:active:translate-y-px focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[var(--pr-focus-ring)] disabled:cursor-not-allowed disabled:border-[var(--pr-border-light)] disabled:bg-[var(--pr-surface-mid)] disabled:text-[var(--pr-text-3)] border-[var(--pr-border)] bg-[var(--pr-border)] text-[var(--pr-text-inv)] enabled:hover:border-[var(--pr-orange)] enabled:hover:bg-[var(--pr-orange)]`

| Property | Value |
| --- | --- |
| font-size | `9px` |
| font-family | `"JetBrains Mono", monospace` |
| padding-top | `0px` |
| padding-bottom | `0px` |
| padding-left | `0px` |
| padding-right | `0px` |
| padding-block | `0px` |
| padding-inline | `0px` |
| background-color | `oklch(0.13 0.005 60)` |
| border-width | `2px` |
| border-radius | `0px` |
| letter-spacing | `0.9px` |

## Ghost Variant · First Button · DEFAULT State

Class attribute: `border-2 border-solid rounded-none shadow-none inline-flex items-center justify-center gap-2 px-5 py-2.5 font-mono text-[9px] font-medium uppercase tracking-[0.1em] transition-[background-color,border-color,color,transform] duration-120 ease-linear cursor-pointer enabled:active:translate-y-px focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[var(--pr-focus-ring)] disabled:cursor-not-allowed disabled:border-[var(--pr-border-light)] disabled:bg-[var(--pr-surface-mid)] disabled:text-[var(--pr-text-3)] border-[var(--pr-border)] bg-transparent text-[var(--pr-text)] enabled:hover:border-[var(--pr-orange)] enabled:hover:bg-[var(--pr-orange-dim)] enabled:hover:text-[var(--pr-orange)]`

| Property | Value |
| --- | --- |
| font-size | `9px` |
| font-family | `"JetBrains Mono", monospace` |
| padding-top | `0px` |
| padding-bottom | `0px` |
| padding-left | `0px` |
| padding-right | `0px` |
| padding-block | `0px` |
| padding-inline | `0px` |
| background-color | `rgba(0, 0, 0, 0)` |
| border-width | `2px` |
| border-radius | `0px` |
| letter-spacing | `0.9px` |

## Dist CSS Utility Checks

| Utility | Selector searched | Present | Matched files |
| --- | --- | --- | --- |
| `rounded-none` | `.rounded-none` | yes | `dist/_astro/press-tailwind.CFStWqdX.css` |
| `border-2` | `.border-2` | yes | `dist/_astro/press-tailwind.CFStWqdX.css` |
| `shadow-none` | `.shadow-none` | yes | `dist/_astro/press-tailwind.CFStWqdX.css` |
| `font-mono` | `.font-mono` | yes | `dist/_astro/press-tailwind.CFStWqdX.css` |
| `text-[9px]` | `.text-\[9px\]` | yes | `dist/_astro/press-tailwind.CFStWqdX.css` |
| `tracking-[0.1em]` | `.tracking-\[0\.1em\]` | yes | `dist/_astro/press-tailwind.CFStWqdX.css` |
| `px-5` | `.px-5` | yes | `dist/_astro/press-tailwind.CFStWqdX.css` |
| `py-2.5` | `.py-2\.5` | yes | `dist/_astro/press-tailwind.CFStWqdX.css` |

## Root Custom Properties

| Property | Computed value |
| --- | --- |
| `--pr-font-mono` | `'JetBrains Mono', monospace` |
| `--pr-font-body` | `'DM Sans', sans-serif` |
| `--pr-font-display` | `'Syne', sans-serif` |
| `--pr-orange` | `oklch(57% 0.205 38)` |
| `--pr-border` | `oklch(13% 0.005 60)` |
| `--pr-bg` | `oklch(97% 0.003 100)` |

## Notes

- CSS utility presence was checked against built `dist/**/*.css` selectors.
- Computed values were captured from the live dev server page.
- The built CSS contains `.px-5` and `.py-2.5`, but the live dev-server buttons still computed `0px` for both physical and logical padding properties.
