---
name: to-guardrails
description: Use when an SDD product workflow needs explicit AI boundaries, source-of-truth order, scope limits, conflict handling, stop conditions, and verification rules.
---
# to-guardrails

## Universal SDD Rule
AI is not the source of truth. Source files and explicit user answers are the source of truth.

If blocker-level information is missing from the source files, do not create or update the output file yet. Use a focused grill-me gap-check first. Resolve the decision tree one branch at a time, ask one question at a time when the answer affects the next question, and include a recommended answer with each question. If the answer can be found by inspecting source files or the codebase, inspect instead of asking. Do not turn guesses into facts.

Create only the final output file. Do not write unverified assumptions into the artifact. Before creating or updating `docs/guardrails.md`, every load-bearing rule must be source-backed, user-confirmed, or left in `Open Questions`.

## Input
Read:
- `README.md`
- `docs/product-idea.md`
- `docs/prd.md`
- `docs/user-journey.md`, if present
- `docs/screen-map.md`, if present
- `docs/wireframes.md`, if present
- `docs/ux-ui-brief.md`, if present
- `docs/terminology.md`, if present
- `docs/project-principles.md`, if present

## Output
Create or update exactly one artifact:
- `docs/guardrails.md`

Do not modify unrelated files.

## Artifact Boundary
`docs/guardrails.md` owns:
- source-of-truth hierarchy
- AI autonomy boundaries
- allowed and forbidden changes
- scope boundaries
- conflict resolution rules
- when to ask before acting
- when to stop
- verification expectations
- document separation rules

It must not define:
- user journey content
- screen inventory
- wireframe layouts
- visual design direction
- QA checklist details
- implementation tasks

Other artifacts may follow these rules, but they must not duplicate this document.

## Proven Mechanics To Use
- Evidence before claims: no success, completion, quality, or compliance claim without fresh verification evidence.
- Spines and source docs win over generated mockups, implementation guesses, and assistant preference.
- Extract, do not ingest: when sources are long, pull only the relevant decisions and cite them. Do not paraphrase entire source files into this artifact.
- Right-size rigor to stakes: hobby, internal, consumer, paid, regulated, accessibility-critical, or safety-sensitive products need different guardrails.
- Define what the AI may decide alone, what it may propose but not finalize, and what requires explicit user approval.
- Preserve artifact boundaries: later docs may reference earlier docs, not silently rewrite them.
- Stop before acting when a named source, visual reference, design system, or requirement cannot be accessed.
- Do not silently ignore unavailable files, screenshots, links, tokens, or brand materials.

## Gap-Check
Before writing, verify that sources identify:
- which documents are authoritative
- what AI may decide independently
- what requires explicit user approval
- what is forbidden
- how conflicts should be resolved
- required verification standard
- which visual/design sources are authoritative, if any
- whether AI may propose aesthetic options or must wait for user-provided direction

If authority, autonomy, forbidden actions, or conflict rules are missing or contradictory, stop and ask grill-me questions before producing the output.

## Workflow
1. Inspect the input files.
2. Identify all available sources of truth.
3. Define source priority from most authoritative to least authoritative.
4. Define AI autonomy boundaries.
5. Define scope boundaries and forbidden behavior.
6. Define visual/design authority rules.
7. Define conflict resolution and stop conditions.
8. Define verification rules for SDD artifacts and future implementation.
9. Preserve strict artifact separation.
10. Create or update only `docs/guardrails.md`.

## Required Output Structure
Use this structure:

```markdown
# Guardrails

## Source References

## Source Of Truth Order

## AI Autonomy Boundaries

## Allowed Changes

## Forbidden Changes

## Scope Boundaries

## Design Authority Rules

## Conflict Resolution

## When To Ask

## When To Stop

## Artifact Separation Rules

## Verification Rules

## Evidence Requirements

## Source Access Failures

## Open Questions
```

## Final Report
Return:
- `Result`
- `Created/Updated File`
- `Confirmed Rules And Constraints`
- `Open Questions`
- `Next Recommended Action`
- `Next Recommended Skill`
