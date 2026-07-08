---
name: to-qa-checklist
description: Use when approved SDD product, UX, architecture, and DoD/eval artifacts exist and the user wants a QA checklist, acceptance checks, accessibility checks, responsive checks, visual regression checks, or release-readiness criteria.
---
# to-qa-checklist

## Universal SDD Rule
AI is not the source of truth. Source files and explicit user answers are the source of truth. Mirror source terminology exactly; when sources use conflicting terms for one concept, do not pick silently - ask or flag it in `Open Questions`, then record the canonical term and aliases to avoid.

If blocker-level information is missing from the source files, do not create or update the output file yet. Use a focused grill-me gap-check first. Resolve the decision tree one branch at a time, ask one question at a time when the answer affects the next question, and include a recommended answer with each question. If the answer can be found by inspecting source files or the codebase, inspect instead of asking. Do not turn guesses into facts.

Create only the final output file. Do not write unverified assumptions into the artifact. Before creating or updating `docs/qa-checklist.md`, every checklist group must be source-backed, user-confirmed, or left in `Open Questions`.

If a gap-check ran, or if the skill synthesized decisions not fully determined by source files, play back the resolved decisions to the user in a pithy summary and proceed only after confirmation. If sources already confirm this exact direction, create the artifact and surface the decisions in the Final Report.

## Input
Read:
- `README.md`, if present
- `docs/prd.md`
- `docs/user-journey.md`
- `docs/screen-map.md`
- `docs/wireframes.md`
- `docs/design-brief.md`
- `docs/architecture.md`, if present from the `to-architecture` step
- `docs/dod-evals.md`, if present from the `to-dod-evals` step
- `docs/guardrails.md`, if present from the `to-guardrails` step

## Output
Create or update exactly one artifact:
- `docs/qa-checklist.md`

Do not modify unrelated files.

## Artifact Boundary
`docs/qa-checklist.md` owns:
- source-backed acceptance checklist
- journey completion checks
- screen and state coverage checks
- UX/UI consistency checks
- responsive checks
- accessibility checks
- browser/device checks
- regression risk checks
- release readiness checks

Evidence policy (when evidence is required, what counts) belongs to `docs/guardrails.md`; this file owns per-check evidence artifacts and cites that policy instead of restating it.

Definition of Done, reusable gates, eval result format, and completion rules belong to `docs/dod-evals.md`; this file owns concrete QA checklist items and cites that contract instead of restating it.

Architecture-driven verification concerns belong to `docs/architecture.md`; this file verifies them through checklist items without redefining architecture.

For states: verify the state list owned by `docs/screen-map.md`; cite it, do not re-derive it.

It must not define:
- new product requirements
- new user journeys
- new screens
- wireframe layout changes
- visual design direction
- architecture decisions
- Definition of Done or reusable eval gates
- implementation tasks

Reference source artifacts instead of repeating their full content.

## Proven Mechanics To Use
- Evidence before claims: the checklist must define what evidence proves each important claim.
- Separate UX risks from accessibility risks and visual polish issues.
- Tie every recommendation back to the user goal, workflow, screen state, or accessibility outcome.
- Do not imply WCAG compliance from screenshots or static docs alone. State verification limits.
- Include complete state checks: default, hover, focus, active, disabled, loading, empty, error, success, long-content, offline, permission-denied, and repeat-click where relevant.
- Include responsive reflow and zoom resilience checks.
- Include keyboard access, focus behavior, labels, instructions, errors, target sizes, motion, timing, and state-change communication.
- For visual QA, compare against source docs, wireframes, design brief, and any approved mockups. Mockups do not override source docs.
- Assign a severity to every check: P0 blocks core use or is a severe accessibility failure; P1 is a major mismatch or usability regression; P2 is moderate drift or a fixable gap; P3 is polish.
- Release readiness is binary: `passed` only when no P0-P2 items remain open; otherwise `blocked` with the blockers named. P3 items may remain as follow-up.
- Use concrete floors as defaults, overridable by sources: touch targets at least 44x44px where touch interaction matters, with at least 8px gaps; text contrast at least 4.5:1 and at least 3:1 for large text in both light and dark themes; mobile input text at least 16px to prevent iOS auto-zoom; body text usually 14-16px depending on product type; visible focus on all interactive elements; no emoji as icons; no horizontal page overflow; reduced-motion respected; breakpoints 390, 430, 768, 1280, and 1440px unless sources specify devices.

## Gap-Check
Before writing, verify that sources identify:
- expected product behavior
- critical user journey
- required screens and states
- UX/UI expectations
- target platforms or browsers, if relevant
- acceptance criteria or equivalent success conditions
- architecture-driven verification concerns, if relevant
- DoD/eval gates, if `docs/dod-evals.md` exists
- accessibility target
- source of visual truth for UI comparison, if any
- verification limits, if some checks require implementation rather than docs

If acceptance criteria, required states, or target platforms are missing and cannot be safely derived from sources, stop and ask grill-me questions before producing the output.

## Workflow
1. Inspect the input files.
2. Derive checks only from approved SDD artifacts.
3. Group checklist items by product behavior, journey, screens, states, UX/UI, responsive, accessibility, and release readiness.
4. Include source references for important checklist groups. `Product Acceptance` items must cite the PRD requirement or user story they verify instead of restating it.
5. Include checks that verify architecture and DoD/eval contracts when `docs/architecture.md` or `docs/dod-evals.md` exist, without redefining those contracts.
6. Include expected evidence for checks that will later require implementation or screenshots.
7. State evidence limits where docs cannot prove runtime behavior.
8. Avoid adding requirements, architecture decisions, DoD rules, or implementation details.
9. Before writing the artifact, verify the planned content:
   - Every checklist group traces to a named source file or an explicit user answer, or it is moved to `Open Questions`.
   - No content belongs to another artifact's ownership per the Artifact Boundary.
   - No placeholder text and no generic filler written to satisfy the template.
10. Create or update only `docs/qa-checklist.md`.

## Required Output Structure
Use this structure:

Required contract sections are `Source References`, `Product Acceptance`, `Screen And State Checks`, `UX/UI Checks`, `Evidence Requirements`, `Evidence Limits`, `Release Readiness`, and `Open Questions`. Optional sections may be omitted when sources give them no content. Required sections may use a single line `Not applicable: <reason>` only when the reason is source-backed. Never fill a section to satisfy the template. Every checklist item carries a severity (P0-P3). `Release Readiness` must conclude with exactly `passed` or `blocked`, with blockers named when blocked. List omitted optional sections in the Final Report.

```markdown
# QA Checklist

## Source References

## Product Acceptance

## User Journey Checks

## Screen And State Checks

## Wireframe Consistency Checks

## UX/UI Checks

## Visual Regression Checks

## Responsive Checks

## Accessibility Checks

## Interaction And State-Change Checks

## Browser And Device Checks

## Evidence Requirements

## Evidence Limits

## Regression Risks

## Release Readiness

## Open Questions
```

## Final Report
Return:
- `Result`
- `Created/Updated File`
- `Confirmed Facts And Constraints`
- `Omitted Optional Sections`, if any
- `Open Questions`
- `Next Recommended Action`
- `Next Recommended Skill`
