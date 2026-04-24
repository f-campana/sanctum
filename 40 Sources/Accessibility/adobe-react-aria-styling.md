---
type: source
source_kind: article
author: Adobe
url: https://react-aria.adobe.com/styling
captured: 2026-04-25
domain: react-aria.adobe.com
status: processed
---

# [Adobe React Aria Styling]

## Summary

Adobe's React Aria styling guide documents how React Aria exposes accessible behavior without imposing a visual system. The page explains that the library is unstyled by default, supports standard `className` and `style` props, exposes interaction state through DOM hooks and render props, and is designed to work with vanilla CSS, utility-class workflows, and CSS-in-JS. This was captured because the accessibility audit identified a gap between behavior and styling in our component-library approach.

## Relevance to this system

This source is directly relevant to a token-driven component library because it shows a clean boundary between accessible interaction logic and brand-specific presentation. React Aria handles keyboard, focus, press, hover, selection, and disabled behavior while exposing those states through stable styling hooks rather than hard-coded visuals. For our system, that suggests the right architecture is not "one monolithic styled widget," but accessible primitives that surface machine-readable state so our tokens and themes can decide the look without reimplementing accessibility logic.

## Key insights

- React Aria's model is accessible primitives with no default visual opinion. Components accept normal styling interfaces, include predictable default class names when needed, and let teams attach their own design tokens, CSS, utility classes, or CSS-in-JS without rewriting the interaction layer.
- Interaction and accessibility state are surfaced explicitly through DOM attributes such as `data-hovered`, `data-pressed`, `data-focused`, and `data-disabled`, along with related state hooks like selection and entry or exit states. This matters for token-driven styling because the visual system can respond to stable semantic state instead of duplicating input-modality logic in CSS and JavaScript.
- The styling API keeps accessibility logic and visuals separable. React Aria owns behavior, focus, and cross-modality interaction semantics, while the product team owns appearance through class names, styles, render props, slots, and CSS variables. For our component library, the derived pattern is to expose stable state hooks at the primitive boundary so visual themes can be swapped without breaking accessible behavior.

## What we derived vs what belongs to them

**Derived (methodology — ours to use):**
- Separate accessible behavior primitives from branded presentation primitives so tokens and themes do not have to reimplement interaction semantics.
- Expose interaction state to styling through stable, declarative DOM hooks that design tokens can target consistently.
- Treat hover, press, focus, disabled, selected, and open or close state as part of the styling contract, not as incidental implementation detail hidden in component internals.
- Use the accessibility layer as the source of truth for behavioral state and let the visual layer subscribe to it.

**Theirs (identity — not ours to replicate):**
- Adobe's React Aria product, documentation structure, component APIs, default class naming scheme, and example code belong to Adobe.
- The exact React Aria render-prop surface, library-specific component names, and Tailwind plugin are product-specific implementation details, not our own system identity.
- Their examples demonstrate the method, but our component contracts, token names, and styling API need to be authored in our own language.

## Follow-up

- [ ] Define a library-wide state exposure contract for styling hooks so tokens can target accessible state consistently across primitives.
- [ ] Review whether our current components leak visual concerns into behavior code and split them where accessibility logic and styling are still entangled.
