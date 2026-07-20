---
name: to-development-plan
description: Use when the current validated product, UX, architecture, DoD/eval, guardrail, and QA SDD artifacts plus the engineer-approved integrated design baseline exist and the user wants a development plan, implementation plan, build order, task breakdown, or verification plan. SDD readiness is not another human approval.
---
# to-development-plan

## Universal SDD Rule
AI is not the source of truth. Source files and explicit user answers are the source of truth. Mirror source terminology exactly; when sources use conflicting terms for one concept, do not pick silently - ask or flag it in `Open Questions`, then record the canonical term and aliases to avoid.

If information is missing from the source files, inspect available sources and the codebase first. Use a focused grill-me gap-check before writing only when the answer is genuinely non-inferable and materially changes product scope or a high-risk boundary. Resolve the decision tree one branch at a time, ask one question at a time, and include a recommended answer. For all other gaps, including pre-approval design ambiguity, use the smallest reversible source-grounded choice, record it, and continue. Do not turn guesses into facts.

Create only the final output file. Do not write unverified assumptions into the artifact. Before creating or updating `docs/development-plan.md`, every implementation unit must be source-backed, user-confirmed, or left in `Open Questions`.

If a gap-check ran, or if the skill synthesized decisions not fully determined by source files, play back the resolved decisions in a pithy summary and continue with the smallest reversible, source-grounded choice unless the missing answer materially changes product scope or a high-risk boundary. Playback is not an approval gate. If planning would change the Approved Visual Baseline, record `baseline_change_required` for the orchestrator; planning must not request or grant design approval itself.

## Input
Read:
- `README.md`, if present
- `docs/prd.md`
- `docs/user-journey.md`
- `docs/screen-map.md`
- `docs/wireframes.md`
- `docs/design-brief.md`
- the canonical `Approved Visual Baseline` section inside `docs/design-brief.md` and the selected prototype artifacts it references; for a UI product, `Status: approved` and a stable Baseline ID are required before production implementation units are created
- `docs/architecture.md`
- `docs/dod-evals.md`
- `docs/guardrails.md`
- `docs/qa-checklist.md`

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
- approved-baseline mapping and permitted visual variance per user-visible unit
- prototype-to-production promotion boundaries when prototype code exists
- frontend/backend interface contracts and integration seams for cross-layer units

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
- Use the PRD and journey artifacts for behavior and scope, and the Approved Visual Baseline for visual composition, interaction detail, and frontend presentation. Architecture, guardrails, and applicable standards remain hard technical and risk boundaries. Do not reinterpret or re-approve the design inside the development plan.
- Treat image-to-code or equivalent prototype output as design evidence and an optional frontend seed, not as proof of production auth, persistence, backend/API, integrations, security boundaries, or exhaustive edge-case behavior. When prototype code will be reused, define a traced promote/diff step and keep Phase 3 frontend, backend, and integration responsibilities explicit.
- Do not turn the plan into tiny commit choreography unless the user asks.

## Gap-Check
Before writing, verify that sources identify:
- current validated product scope
- current validated screens and states
- approved visual-baseline status, Baseline ID, selected candidate/version, immutable visual-target reference/hash, prototype references, covered screens/states/viewports, and permitted variance for UI products
- UX/UI expectations
- implementation constraints or stack, if available
- architecture constraints, if available
- DoD/eval gates, if available
- acceptance or QA criteria
- required verification commands, if available
- existing architecture, file structure, or component system when a codebase exists
- deployment or runtime constraints that affect build order
- prototype-code reuse policy and missing production capabilities, when runnable prototype code exists

If stack, constraints, dependencies, or verification expectations are missing, first re-invoke the owning upstream artifact skill. Ask only when the unresolved answer materially changes product scope or a high-risk boundary. Otherwise use the smallest reversible source-compatible plan seam, record the dependency, and continue.

## Workflow
1. Inspect the input files.
2. Extract implementation scope only from current validated SDD artifacts.
3. Resolve the canonical `Approved Visual Baseline` section in `docs/design-brief.md` and verify `Status: approved`, its stable Baseline ID, selected candidate/version, immutable visual-target reference/hash, approval receipt, and referenced prototype artifacts. For a UI product, stop before creating production units if this whole-baseline approval is absent; do not ask for any additional design approval. A changed or superseded Baseline ID invalidates affected plan units and requires the QA checklist plus those units to be regenerated before execution continues.
4. Inspect the codebase structure if implementation will happen in an existing project.
5. Use `docs/architecture.md` as the architecture source of truth; do not re-decide architecture inside the plan.
6. Use `docs/dod-evals.md` as the Definition of Done and eval-gate source of truth; do not redefine gates inside the plan.
7. Map likely files, modules, routes, components, services, and tests before defining tasks.
8. Break work into implementation units that can be built and verified.
9. Order units by dependency and user-value sequence.
10. Attach behavioral SDD references and, for every user-visible unit, Approved Baseline ID, covered screens/states, design contract, permitted variance, and visual-fidelity verification. For backend-only units, state whether the unit enables user-visible states, data, or actions. When prototype code exists, identify whether the unit reuses none of it or promotes a traced diff, and name every production capability still implemented outside the prototype. For every cross-layer or independently parallelizable frontend/backend unit, name interfaces produced and consumed, API/data-contract references, ownership, compatibility expectations, and integration verification.
11. Include verification steps derived from `docs/qa-checklist.md` and `docs/dod-evals.md`.
12. Self-review coverage: every PRD requirement and every screen and state in `docs/screen-map.md` maps to an implementation unit or to Out Of Scope / Open Questions with a reason; the Approved Visual Baseline maps to every user-visible unit; architecture constraints from `docs/architecture.md` and DoD/eval gates from `docs/dod-evals.md` map to verification or sequencing notes; cross-layer interfaces have both a producer and consumer; unit names and references are consistent across the plan; no placeholders remain.
13. Avoid tiny commit choreography as the main teaching frame.
14. Avoid adding product scope, architecture decisions, DoD rules, or design decisions.
15. Before writing the artifact, verify the planned content:
   - Every implementation unit traces to a named source file or an explicit user answer, or it is moved to `Open Questions`.
   - No content belongs to another artifact's ownership per the Artifact Boundary.
   - No placeholder text and no generic filler written to satisfy the template.
16. Create or update only `docs/development-plan.md`.

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
- `Delivery Layer: frontend | backend | full-stack | integration | infrastructure`
- `Approved Baseline ID`, for user-visible units
- `Baseline Screens And States`, for user-visible units
- `Design Contract And Permitted Variance`, for user-visible units
- `Visual Fidelity Verification`, for user-visible units
- `Baseline Impact: none | user-visible states/data/actions enabled`, for backend-only units
- `Prototype Reuse: none | traced promote/diff`, when prototype code exists
- `Production Capabilities Added Beyond Prototype`, when prototype code exists
- `Interfaces Produced`, for cross-layer or independently parallelized units
- `Interfaces Consumed`, for cross-layer or independently parallelized units
- `API/Data Contract References`, for cross-layer or independently parallelized units
- `Interface Owner`, for cross-layer or independently parallelized units
- `Compatibility Expectations`, for cross-layer or independently parallelized units
- `Integration Verification`, for cross-layer or independently parallelized units

## Final Report
Return:
- `Result`
- `Created/Updated File`
- `Confirmed Facts And Constraints`
- `Omitted Optional Sections`, if any
- `Open Questions`
- `Next Recommended Action`
- `Next Recommended Skill`
