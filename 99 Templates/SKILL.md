---
name: domain/action
version: 1.0.0
type: producer          # producer | validator | workflow
domain: domain          # design | wiki | docs | react | typescript | express | github | memory | architecture | security
tier: action            # action | workflow | project
triggers:
  - /domain-action
  - "natural language trigger phrase"
reads_from: path/to/input
writes_to: path/to/output
model_preference: claude-sonnet  # claude-sonnet | claude-opus | local
---

# domain/action

## When to use

Describe the specific conditions that trigger this skill. Be precise enough
that an agent can determine whether to load it without reading further.
One short paragraph. No bullet lists here — the trigger is a situation, not
a checklist.

## What it does

Numbered steps. Each step is one concrete action.

1. Reads [specific input] from [specific location].
2. Does [specific transformation or operation].
3. Writes [specific output] to [specific location].
4. Reports: "[short completion statement with key facts]."

## What it does NOT do

- Does not [nearest confusable action — the thing an agent might try to do
  if it expanded scope].
- Does not [second confusable action].
- Does not modify files it did not create.

## Inputs

**Required:**
- `[input-name]` — description, format, location.

**Optional:**
- `[optional-input]` — description, when it applies.

## Output

One [artifact type] at `[path/to/output]`.

Format: [describe the output format — markdown, JSON, HTML, etc.]

## Failure modes

**[Failure condition 1]:** [How to handle it — stop, request clarification,
proceed with documented assumption.]

**[Failure condition 2]:** [How to handle it.]

**Scope creep:** If the task requires actions outside this skill's scope,
stop and surface the boundary rather than expanding.
