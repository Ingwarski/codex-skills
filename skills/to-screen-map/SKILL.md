---
name: to-screen-map
description: Use when docs/prd.md and docs/user-journey.md exist and the next SDD artifact should close the product's screens, surfaces, routes, states, and transitions.
---
# to-screen-map

## Universal SDD Rule
AI is not the source of truth. Source files and explicit user answers are the source of truth.

If blocker-level information is missing from the source files, do not create or update the output file yet. Use a focused grill-me gap-check first. Resolve the decision tree one branch at a time, ask one question at a time when the answer affects the next question, and include a recommended answer with each question. If the answer can be found by inspecting source files or the codebase, inspect instead of asking. Do not turn guesses into facts.

Create only the final output file. Do not write unverified assumptions into the artifact. Before creating or updating `docs/screen-map.md`, every load-bearing claim must be source-backed, user-confirmed, or left in `Open Questions`.

## Input
Read:
- `README.md`
- `docs/product-idea.md`
- `docs/prd.md`
- `docs/user-journey.md`
- `docs/terminology.md`, if present
- `docs/project-principles.md`, if present
- `docs/guardrails.md`, if present

## Output
Create or update exactly one artifact:
- `docs/screen-map.md`

Do not modify unrelated files.

## Artifact Boundary
`docs/screen-map.md` owns:
- product screens and surfaces
- routes or navigation locations
- entry points and exit points
- transitions between screens
- required screen states
- empty, loading, error, success, and permission states
- links from screens to PRD requirements and journey stages

It must not define:
- detailed screen layouts
- component hierarchy inside a screen
- final copy
- visual style, colors, typography, or design tokens
- QA checklist items
- implementation tasks

Later artifacts may reference this file, but they must not duplicate its content.

## Proven Mechanics To Use
- Apply surface closure: every stated journey need must have a screen, surface, system response, or explicit non-screen explanation.
- Apply scope closure: every screen must trace back to `docs/prd.md` or `docs/user-journey.md`.
- Treat screens as contracts, not layouts. A screen map says what exists and how it connects; wireframes decide the internal structure.
- Model states explicitly. At minimum consider empty, loading, error, success, permission-denied, offline, and long-content states when relevant.
- Use Mermaid `flowchart LR` for transitions when it clarifies the route graph.
- Use a matrix for journey stage to screen coverage when the workflow has more than three screens.

## Gap-Check
Before writing, verify that sources identify:
- core screens needed to complete the main journey
- required navigation or route model
- completion, cancellation, error, and return paths
- important state transitions
- any modal, drawer, notification, email, or system surface that is required to complete the journey
- whether the product is single-surface, multi-surface, mobile, web, desktop, or cross-device

If routes, completion paths, or state logic are missing or contradictory, stop and ask grill-me questions before producing the output.

## Workflow
1. Inspect the input files.
2. Extract the product's main workflow from `docs/prd.md` and `docs/user-journey.md`.
3. Identify all screens and surfaces required for the MVP journey.
4. Map entry points, exits, transitions, and return paths.
5. Identify required screen states.
6. Build a journey-to-screen coverage matrix.
7. Check surface closure: every journey stage must have a supporting screen or explicit non-screen explanation.
8. Check scope closure: every screen must trace to the PRD or user journey.
9. Flag screens or states that would require new product scope.
10. Create or update only `docs/screen-map.md`.

## Required Output Structure
Use this structure:

```markdown
# Screen Map

## Source References

## Screen Inventory

## Surface Closure Matrix

## Route Map

## Navigation Model

## Journey-To-Screen Trace

## Screen States

## Transition Notes

## Entry And Exit Points

## Edge Paths

## Out Of Scope Screens

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
