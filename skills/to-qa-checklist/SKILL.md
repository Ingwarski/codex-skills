---
name: to-qa-checklist
description: Use when approved SDD product and UX artifacts exist and the next artifact should define source-backed QA, UX, accessibility, responsive, state, and release-readiness checks.
---
# to-qa-checklist

## Universal SDD Rule
AI is not the source of truth. Source files and explicit user answers are the source of truth.

If blocker-level information is missing from the source files, do not create or update the output file yet. Use a focused grill-me gap-check first. Resolve the decision tree one branch at a time, ask one question at a time when the answer affects the next question, and include a recommended answer with each question. If the answer can be found by inspecting source files or the codebase, inspect instead of asking. Do not turn guesses into facts.

Create only the final output file. Do not write unverified assumptions into the artifact. Before creating or updating `docs/qa-checklist.md`, every checklist group must be source-backed, user-confirmed, or left in `Open Questions`.

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
- `docs/terminology.md`, if present
- `docs/project-principles.md`, if present

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

It must not define:
- new product requirements
- new user journeys
- new screens
- wireframe layout changes
- visual design direction
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
- For visual QA, compare against source docs, wireframes, UX/UI brief, and any approved mockups. Mockups do not override source docs.

## Gap-Check
Before writing, verify that sources identify:
- expected product behavior
- critical user journey
- required screens and states
- UX/UI expectations
- target platforms or browsers, if relevant
- acceptance criteria or equivalent success conditions
- accessibility target
- source of visual truth for UI comparison, if any
- verification limits, if some checks require implementation rather than docs

If acceptance criteria, required states, or target platforms are missing and cannot be safely derived from sources, stop and ask grill-me questions before producing the output.

## Workflow
1. Inspect the input files.
2. Derive checks only from approved SDD artifacts.
3. Group checklist items by product behavior, journey, screens, states, UX/UI, responsive, accessibility, and release readiness.
4. Include source references for important checklist groups.
5. Include expected evidence for checks that will later require implementation or screenshots.
6. State evidence limits where docs cannot prove runtime behavior.
7. Avoid adding requirements or implementation details.
8. Create or update only `docs/qa-checklist.md`.

## Required Output Structure
Use this structure:

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
- `Open Questions`
- `Next Recommended Action`
- `Next Recommended Skill`
