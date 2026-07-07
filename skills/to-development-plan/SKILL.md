---
name: to-development-plan
description: Use when approved SDD product, UX, guardrail, and QA artifacts exist and the next artifact should define implementation units, dependencies, acceptance checks, and verification order.
---
# to-development-plan

## Universal SDD Rule
AI is not the source of truth. Source files and explicit user answers are the source of truth.

If blocker-level information is missing from the source files, do not create or update the output file yet. Use a focused grill-me gap-check first. Resolve the decision tree one branch at a time, ask one question at a time when the answer affects the next question, and include a recommended answer with each question. If the answer can be found by inspecting source files or the codebase, inspect instead of asking. Do not turn guesses into facts.

Create only the final output file. Do not write unverified assumptions into the artifact. Before creating or updating `docs/development-plan.md`, every implementation unit must be source-backed, user-confirmed, or left in `Open Questions`.

## Input
Read:
- `README.md`
- `docs/product-idea.md`
- `docs/prd.md`
- `docs/user-journey.md`
- `docs/screen-map.md`
- `docs/wireframes.md`
- `docs/ux-ui-brief.md`
- `docs/guardrails.md`, if present
- `docs/qa-checklist.md`, if present
- `docs/terminology.md`, if present
- `docs/project-principles.md`, if present

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
- acceptance or QA criteria
- required verification commands, if available
- existing architecture, file structure, or component system when a codebase exists
- deployment or runtime constraints that affect build order

If stack, constraints, dependencies, or verification expectations are missing and materially affect the plan, stop and ask grill-me questions before producing the output.

## Workflow
1. Inspect the input files.
2. Extract implementation scope only from approved SDD artifacts.
3. Inspect the codebase structure if implementation will happen in an existing project.
4. Map likely files, modules, routes, components, services, and tests before defining tasks.
5. Break work into implementation units that can be built and verified.
6. Order units by dependency and user-value sequence.
7. Attach source references and acceptance checks to every unit.
8. Include verification steps derived from `docs/qa-checklist.md` when present.
9. Avoid tiny commit choreography as the main teaching frame.
10. Avoid adding product scope or design decisions.
11. Create or update only `docs/development-plan.md`.

## Required Output Structure
Use this structure:

```markdown
# Development Plan

## Source References

## Implementation Strategy

## Codebase Map

## Implementation Units

## Dependency Order

## Acceptance Checks

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
- `Open Questions`
- `Next Recommended Action`
- `Next Recommended Skill`
