---
name: to-user-journey
description: Use when docs/prd.md exists and the next SDD artifact should clarify the real user journey before screens, wireframes, visual design, QA, or implementation planning.
---
# to-user-journey

## Universal SDD Rule
AI is not the source of truth. Source files and explicit user answers are the source of truth.

If blocker-level information is missing from the source files, do not create or update the output file yet. Use a focused grill-me gap-check first. Resolve the decision tree one branch at a time, ask one question at a time when the answer affects the next question, and include a recommended answer with each question. If the answer can be found by inspecting source files or the codebase, inspect instead of asking. Do not turn guesses into facts.

Create only the final output file. Do not write unverified assumptions into the artifact. Before creating or updating `docs/user-journey.md`, every load-bearing claim must be source-backed, user-confirmed, or left in `Open Questions`.

## Input
Read:
- `README.md`
- `docs/product-idea.md`
- `docs/prd.md`
- `docs/terminology.md`, if present
- `docs/project-principles.md`, if present
- `docs/guardrails.md`, if present

## Output
Create or update exactly one artifact:
- `docs/user-journey.md`

Do not modify unrelated files.

## Artifact Boundary
`docs/user-journey.md` owns:
- primary user and context
- user goal and motivation
- named protagonist for the main journey
- real-session framing
- journey stages
- user actions
- decision points
- friction, fears, and blockers
- exit points
- success and failure states
- climax beat: the moment the user gets value or hits the central friction
- MVP journey risks

It must not define:
- screen inventory or routes
- wireframe layouts
- visual style, colors, typography, or design tokens
- QA checklist items
- implementation tasks

Later artifacts may reference this file, but they must not duplicate its content.

## Proven Mechanics To Use
- Start from a real person doing a real thing, not from a feature list.
- Use a named protagonist when the sources support it. If the name is unknown, ask or use a role label until confirmed.
- Mirror source terminology exactly. Do not rename user types, workflow steps, or product concepts for style.
- Capture the journey as numbered steps with a climax beat and, where relevant, a failure path.
- Probe for stakes early: hobby, internal tool, consumer product, regulated product, paid workflow, sensitive data, or accessibility-critical usage.
- Prefer a Mermaid `journey` diagram when it clarifies the flow, but keep the markdown artifact readable without the diagram.

## Gap-Check
Before writing, verify that sources identify:
- the primary user
- the user's main goal
- the starting context
- the expected end state
- important constraints or risks
- the form factor or usage context, if it affects the journey
- the user's main fear, friction, or trust concern, if the PRD depends on behavior change

If any of these are missing or contradictory, stop and ask grill-me questions before producing the output.

## Workflow
1. Inspect the input files.
2. Identify the primary user from sources.
3. Identify the real session: where the user is, what triggers the session, what device or context matters, and what pressure exists.
4. Extract the main user goal, success state, and failure path.
5. Map the journey stages from entry to completion as numbered steps.
6. Name the climax beat.
7. Capture actions, decisions, friction, trust concerns, exit points, and risks.
8. Trace every claim to source files or explicit user answers.
9. Avoid adding features, personas, flows, or goals outside the PRD.
10. Create or update only `docs/user-journey.md`.

## Required Output Structure
Use this structure:

```markdown
# User Journey

## Source References

## Primary User

## Named Protagonist

## User Goal

## Starting Context

## Stakes And Constraints

## Journey Overview

## Journey Stages

## Climax Beat

## Decision Points

## Friction And Risks

## Failure Path

## Exit Points

## Success State

## Confirmed Facts And Constraints

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
