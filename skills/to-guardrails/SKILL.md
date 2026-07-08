---
name: to-guardrails
description: Use when an SDD workflow needs AI guardrails, source-of-truth order, autonomy limits, scope boundaries, conflict resolution, stop conditions, or verification rules. Can run any time after docs/prd.md exists; running it before the design artifacts is recommended.
---
# to-guardrails

## Universal SDD Rule
AI is not the source of truth. Source files and explicit user answers are the source of truth. Mirror source terminology exactly; when sources use conflicting terms for one concept, do not pick silently - ask or flag it in `Open Questions`, then record the canonical term and aliases to avoid.

If blocker-level information is missing from the source files, do not create or update the output file yet. Use a focused grill-me gap-check first. Resolve the decision tree one branch at a time, ask one question at a time when the answer affects the next question, and include a recommended answer with each question. If the answer can be found by inspecting source files or the codebase, inspect instead of asking. Do not turn guesses into facts.

Create only the final output file. Do not write unverified assumptions into the artifact. Before creating or updating `docs/guardrails.md`, every load-bearing rule must be source-backed, user-confirmed, or left in `Open Questions`.

If a gap-check ran, or if the skill synthesized decisions not fully determined by source files, play back the resolved decisions to the user in a pithy summary and proceed only after confirmation. If sources already confirm this exact direction, create the artifact and surface the decisions in the Final Report.

## Input
Read:
- `README.md`, if present
- `docs/prd.md`
- `docs/user-journey.md`, if present
- `docs/screen-map.md`, if present
- `docs/wireframes.md`, if present
- `docs/ux-ui-brief.md`, if present
- `docs/architecture.md`, if present from the `to-architecture` step
- `docs/dod-evals.md`, if present from the `to-dod-evals` step

This skill can run any time after `docs/prd.md` exists. Running it before the design artifacts is recommended, so they are produced under these guardrails. Re-run it after the UX artifacts exist to add design-authority rules.

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
- mockup, prototype, screenshot, and static-surface limits for completion claims

This file owns the behavioral evidence policy: when the AI must verify, what counts as evidence, and when missing evidence must stop work. `docs/dod-evals.md` owns the reusable completion/eval contract: which gates and evidence make work Done. `docs/qa-checklist.md` owns concrete per-release or per-screen checks and per-check evidence artifacts that cite both.

It must not define:
- user journey content
- screen inventory
- wireframe layouts
- visual design direction
- QA checklist details
- implementation tasks

Other artifacts may follow these rules, but they must not duplicate this document.

## Proven Mechanics To Use
- Evidence before claims, as an operational gate: identify what proves the claim, run it fresh, read the full output, and only then state the result with the evidence. No success, completion, quality, or compliance claim without this sequence.
- Spines and source docs win over generated mockups, implementation guesses, and assistant preference.
- A mockup, screenshot, prototype, or visually convincing static surface is design/visual evidence only; it is not completed functionality unless connected to source-backed behavior, real state/data/actions, runner evidence, and required DoD gates.
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
- where visual/static evidence ends and functionality evidence begins
- which visual/design sources are authoritative, if any
- whether AI may propose aesthetic options or must wait for user-provided direction

If authority, autonomy, forbidden actions, or conflict rules are missing or contradictory, stop and ask grill-me questions before producing the output.

### Default Baseline For Recommendations
Sources rarely state guardrails explicitly. Do not run an open-ended interview. Identify the stakes tier first, present the matching baseline as the recommended answer for each gap-check question, and grill only on deviations and items the user marks as sensitive.

- Hobby / internal: AI may decide layout details, copy proposals, and technical structure alone; proposes scope and visual direction; user approves scope changes and deletions.
- Consumer / paid: AI proposes but does not finalize visual direction, scope, terminology, or anything user-facing; user approves before artifacts change; evidence required for completion claims.
- Regulated / accessibility-critical / sensitive data: AI decides nothing user-facing alone; every claim source-backed; accessibility and compliance items always require explicit user approval and named evidence.

## Workflow
1. Inspect the input files.
2. Identify all available sources of truth.
3. Define source priority from most authoritative to least authoritative.
4. Define AI autonomy boundaries.
5. Define scope boundaries and forbidden behavior.
6. Define visual/design authority rules.
7. Define conflict resolution and stop conditions.
8. Define verification rules for SDD artifacts and future implementation.
9. Define mockup, prototype, screenshot, and static-surface limits for completion claims.
10. Preserve strict artifact separation.
11. Before writing the artifact, verify the planned content:
   - Every load-bearing rule traces to a named source file or an explicit user answer, or it is moved to `Open Questions`.
   - No content belongs to another artifact's ownership per the Artifact Boundary.
   - No placeholder text and no generic filler written to satisfy the template.
12. Create or update only `docs/guardrails.md`.

## Required Output Structure
Use this structure:

Required contract sections are `Source References`, `Source Of Truth Order`, `AI Autonomy Boundaries`, `Forbidden Changes`, `When To Ask`, `When To Stop`, `Artifact Separation Rules`, `Verification Rules`, and `Open Questions`. Optional sections may be omitted when sources give them no content. Required sections may use a single line `Not applicable: <reason>` only when the reason is source-backed. Never fill a section to satisfy the template. List omitted optional sections in the Final Report.

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
- `Omitted Optional Sections`, if any
- `Open Questions`
- `Next Recommended Action`
- `Next Recommended Skill`
