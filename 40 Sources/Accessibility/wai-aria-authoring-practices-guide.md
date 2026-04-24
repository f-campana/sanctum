---
type: source
source_kind: article
author: W3C ARIA Authoring Practices Task Force
url: https://www.w3.org/WAI/ARIA/apg/
captured: 2026-04-25
domain: w3.org
status: processed
---

# [WAI-ARIA Authoring Practices Guide]

## Summary

The WAI-ARIA Authoring Practices Guide (APG) is W3C guidance maintained by the ARIA Authoring Practices Task Force for the ARIA Working Group. It is an informative guide, not a normative standard, and it translates ARIA requirements plus established desktop keyboard conventions into practical widget patterns, examples, and focus-management guidance. This capture specifically reviewed the introduction, ARIA basics, keyboard interface guidance, and the Button, Dialog (Modal), and Listbox patterns because the knowledge OS audit identified an accessibility gap in component behavior.

## Relevance to this system

This source matters because our component library cannot treat accessibility as styling garnish or post-hoc QA. The APG gives the behavior contract we need for interactive primitives: which element owns focus, which keys move or activate it, when focus stays put versus moves into a new context, and which ARIA roles, states, and properties communicate meaning to assistive technology. For our library specifically, this means buttons, dialogs, and listbox-like composites need explicit keyboard models, stable focus return rules, and a clear separation between native HTML semantics and ARIA augmentation so that accessibility behavior is implemented once at the primitive level instead of improvised per product surface.

## Key insights

- The APG is maintained by the W3C ARIA Authoring Practices Task Force for the ARIA Working Group and exists to synthesize ARIA, HTML, CSS, and assistive-technology guidance into usable widget patterns. It is informative rather than normative, but it should still be treated as the practical contract for common widget behavior because it defines the expected keyboard model authors must implement themselves.
- The APG frames ARIA as accessibility semantics made of roles, properties, and states, and it treats every ARIA role as a promise of matching behavior. For our library, that means a `button` must support `Enter` and `Space`, a modal dialog must trap `Tab` and `Shift+Tab`, close on `Escape`, move focus inside on open, and return focus logically on close, and a listbox must keep only one tab stop while using arrow-key navigation with either roving `tabindex` or `aria-activedescendant`.
- The widget pages make focus management concrete instead of abstract. Buttons keep or move focus according to the action they trigger, modal dialogs render outside content inert and require deliberate initial and return focus decisions, and listboxes use selection-aware entry focus plus standard key bindings such as arrow keys, `Home`, `End`, and type-ahead. Our component library should therefore ship primitives with baked-in focus ownership, documented key maps per widget class, and tests that verify those contracts across keyboard-only flows.

## What we derived vs what belongs to them

**Derived (methodology — ours to use):**
- Treat accessibility behavior as a first-class component contract: every interactive primitive needs a documented focus model, key map, and state model.
- Prefer native HTML semantics first, then use ARIA only where native elements do not express the required interaction pattern.
- Implement shared internal utilities for composite focus management, including roving `tabindex`, focus restore on dismiss, and state-driven assistive-technology attributes.
- Add component acceptance tests that verify APG-aligned keyboard interaction for buttons, dialogs, listboxes, and any custom composite derived from them.

**Theirs (identity — not ours to replicate):**
- The APG itself, its page structure, its examples, its wording, and its named W3C guidance artifacts belong to W3C.
- W3C's specific pattern library, editorial framing, and example implementations are reference material, not our design system.
- Any direct copying of APG prose, example code, or branded framing would be replication of W3C material rather than our own library documentation.

## Follow-up

- [ ] Audit every component-library primitive against APG expectations for focus entry, focus exit, and supported keyboard commands.
- [ ] Define which composites will use roving `tabindex` and which will use `aria-activedescendant`, then encode that choice in the library architecture rather than per-component ad hoc logic.
