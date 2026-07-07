---
name: to-development-plan
description: Use when approved SDD product, UX, architecture, DoD/eval, guardrail, and QA artifacts exist and the user wants a development plan, implementation plan, build order, task breakdown, or verification plan.
---
# to-development-plan

## Universal SDD Rule
AI is not the source of truth. Source files and explicit user answers are the source of truth. Mirror source terminology exactly; when sources use conflicting terms for one concept, do not pick silently - ask or flag it in `Open Questions`, then record the canonical term and aliases to avoid.

If blocker-level information is missing from the source files, do not create or update the output file yet. Use a focused grill-me gap-check first. Resolve the decision tree one branch at a time, ask one question at a time when the answer affects the next question, and include a recommended answer with each question. If the answer can be found by inspecting source files or the codebase, inspect instead of asking. Do not turn guesses into facts.

Create only the final output file. Do not write unverified assumptions into the artifact. Before creating or updating `docs/development-plan.md`, every implementation unit must be source-backed, user-confirmed, or left in `Open Questions`.

If a gap-check ran, or if the skill synthesized decisions not fully determined by source files, play back the resolved decisions to the user in a pithy summary and proceed only after confirmation. If sources already confirm this exact direction, create the artifact and surface the decisions in the Final Report.

## Input
Read:
- `README.md`, if present
- `docs/prd.md`
- `docs/user-journey.md`
- `docs/screen-map.md`
- `docs/wireframes.md`
- `docs/ux-ui-brief.md`
- `docs/architecture.md`, if present from the `to-architecture` step
- `docs/dod-evals.md`, if present from the `to-dod-evals` step
- `docs/guardrails.md`, if present from the `to-guardrails` step
- `docs/qa-checklist.md`, if present

## Output
Create or update exactly one artifact:
- `docs/development-plan.md`

Do not modify unrelated files.

## Artifact Boundary
`docs/development-plan.md` owns:
- implementation units
- build order
- dependencies
- source references per unit
- acceptance checks per unit
- verification steps
- risk sequencing
- handoff notes for implementation

It must not define:
- new product requirements
- new user journeys
- new screens
- wireframe changes
- visual design changes
- architecture decisions
- Definition of Done or reusable eval gates
- QA checklist details beyond references

This is an SDD development plan. It may include tests and verification, but it must not reframe the workflow as TDD-first unless the source documents explicitly require that.

## Proven Mechanics To Use
- Start from source-backed scope, not engineering imagination.
- Map files or modules before tasks when a codebase exists. Follow established patterns before proposing new abstractions.
- Break work into small implementation units with clear ownership, dependency order, acceptance checks, and verification evidence.
- Avoid placeholders: no TBD, TODO, "handle edge cases", "write tests for this", or undefined future decisions.
- Every unit needs source references, work items, acceptance checks, and verification.
- Evidence before completion: the plan must say what proves each unit is done.
- SDD-first: tests and verification support the agreed spec; they do not become the source of product truth.
- Do not turn the plan into tiny commit choreography unless the user asks.

## Gap-Check
Before writing, verify that sources identify:
- approved product scope
- approved screens and states
- UX/UI expectations
- implementation constraints or stack, if available
- architecture constraints, if available
- DoD/eval gates, if available
- acceptance or QA criteria
- required verification commands, if available
- existing architecture, file structure, or component system when a codebase exists
- deployment or runtime constraints that affect build order

If stack, constraints, dependencies, or verification expectations are missing and materially affect the plan, stop and ask grill-me questions before producing the output.

## Workflow
1. Inspect the input files.
2. Extract implementation scope only from approved SDD artifacts.
3. Inspect the codebase structure if implementation will happen in an existing project.
4. Use `docs/architecture.md` as the architecture source of truth when present; do not re-decide architecture inside the plan.
5. Use `docs/dod-evals.md` as the Definition of Done and eval-gate source of truth when present; do not redefine gates inside the plan.
6. Map likely files, modules, routes, components, services, and tests before defining tasks.
7. Break work into implementation units that can be built and verified.
8. Order units by dependency and user-value sequence.
9. Attach source references and acceptance checks to every unit.
10. Include verification steps derived from `docs/qa-checklist.md` and `docs/dod-evals.md` when present.
11. Self-review coverage: every PRD requirement and every screen and state in `docs/screen-map.md` maps to an implementation unit or to Out Of Scope / Open Questions with a reason; architecture constraints from `docs/architecture.md` and DoD/eval gates from `docs/dod-evals.md` map to verification or sequencing notes when present; unit names and references are consistent across the plan; no placeholders remain.
12. Avoid tiny commit choreography as the main teaching frame.
13. Avoid adding product scope, architecture decisions, DoD rules, or design decisions.
14. Before writing the artifact, verify the planned content:
   - Every implementation unit traces to a named source file or an explicit user answer, or it is moved to `Open Questions`.
   - No content belongs to another artifact's ownership per the Artifact Boundary.
   - No placeholder text and no generic filler written to satisfy the template.
15. Create or update only `docs/development-plan.md`.

## Required Output Structure
Use this structure:

Required contract sections are `Source References`, `Implementation Strategy`, `Implementation Units`, `Dependency Order`, `Verification Plan`, `Out Of Scope`, and `Open Questions`. Optional sections may be omitted when sources give them no content. Required sections may use a single line `Not applicable: <reason>` only when the reason is source-backed. Never fill a section to satisfy the template. List omitted optional sections in the Final Report.

```markdown
# Development Plan

## Source References

## Implementation Strategy

## Codebase Map

## Implementation Units

## Dependency Order

## Verification Plan

## Visual And UX Verification

## Risks And Sequencing Notes

## Out Of Scope

## Open Questions
```

For each implementation unit include:
- `Unit`
- `Purpose`
- `Source References`
- `Depends On`
- `Work Items`
- `Acceptance Checks`
- `Verification`

## Final Report
Return:
- `Result`
- `Created/Updated File`
- `Confirmed Facts And Constraints`
- `Omitted Optional Sections`, if any
- `Open Questions`
- `Next Recommended Action`
- `Next Recommended Skill`
