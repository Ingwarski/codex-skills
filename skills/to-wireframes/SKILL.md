---
name: to-wireframes
description: Use when docs/screen-map.md exists and the next SDD artifact should define low-fidelity screen structure, hierarchy, CTAs, fields, and state variants before visual design.
---
# to-wireframes

## Universal SDD Rule
AI is not the source of truth. Source files and explicit user answers are the source of truth.

If blocker-level information is missing from the source files, do not create or update the output file yet. Use a focused grill-me gap-check first. Resolve the decision tree one branch at a time, ask one question at a time when the answer affects the next question, and include a recommended answer with each question. If the answer can be found by inspecting source files or the codebase, inspect instead of asking. Do not turn guesses into facts.

Create only the final output file. Do not write unverified assumptions into the artifact. Before creating or updating `docs/wireframes.md`, every load-bearing claim must be source-backed, user-confirmed, or left in `Open Questions`.

## Input
Read:
- `README.md`
- `docs/product-idea.md`
- `docs/prd.md`
- `docs/user-journey.md`
- `docs/screen-map.md`
- `docs/terminology.md`, if present
- `docs/project-principles.md`, if present
- `docs/guardrails.md`, if present

## Output
Create or update exactly one artifact:
- `docs/wireframes.md`

Do not modify unrelated files.

## Artifact Boundary
`docs/wireframes.md` owns:
- low-fidelity screen structure
- content hierarchy
- primary and secondary CTAs
- forms, fields, and inputs
- content zones and repeated blocks
- state variants per screen
- interaction notes needed to understand layout behavior

It must not define:
- final colors
- typography system
- visual mood
- brand style
- component visual polish
- design tokens
- QA checklist items
- implementation tasks

The final product goal is high-quality UX/UI design. This artifact supports that goal by making the product structure clear before visual decisions are made.

## Proven Mechanics To Use
- Run a design-brief gate before wireframing: confirm what each screen must help the user do, what visual or product system should be respected, and how interactive the final experience is expected to be.
- Prefer source capture over guessing. If an existing product, design system, screenshot, Storybook, component library, or token file exists, use it as grounding material.
- Differentiate structure before style: vary hierarchy, grouping, interaction model, and CTA emphasis before discussing brand style.
- Use this separation priority inside wireframes: spacing, grouping, alignment, and hierarchy first; simple dividers second; subtle surface tint third; borders fourth; shadows last.
- Do not default to a whole-app card, nested cards, or card-heavy layouts unless sources require it.
- Include complete structural states: default, loading, empty, error, success, disabled, permission-denied, offline, and long-content where relevant.
- Keep realistic content slots. Avoid lorem ipsum as a decision substitute.

## Gap-Check
Before writing, verify that sources identify:
- the screen inventory
- primary action per screen
- required content or data per screen
- required states per screen
- priority of blocks when space is constrained
- whether an existing design system or component set must be respected
- expected interactivity depth for the later implementation

If block priority, CTAs, forms, or state behavior are missing or contradictory, stop and ask grill-me questions before producing the output.

## Workflow
1. Inspect the input files.
2. Use `docs/screen-map.md` as the source for screens and states.
3. For each screen, define purpose, user intent, content hierarchy, CTAs, inputs, and state variants.
4. Keep wireframes low-fidelity and structural.
5. Define responsive structural behavior only where it affects content priority or interaction.
6. Preserve traceability to PRD requirements, user journey stages, and screen-map entries.
7. Avoid adding features, screens, fields, or flows outside approved sources.
8. Create or update only `docs/wireframes.md`.

## Required Output Structure
Use this structure:

```markdown
# Wireframes

## Source References

## Wireframe Principles

## Screen Blueprints

## Responsive Structure Notes

## Shared Patterns

## State Variants

## Content Priority Notes

## Notes For UX/UI Brief

## Open Questions
```

For each screen blueprint include:
- `Source Screen`
- `Purpose`
- `Primary User Intent`
- `Layout Structure`
- `Primary CTA`
- `Secondary Actions`
- `Inputs And Content`
- `States`
- `Notes For UX/UI Brief`

## Final Report
Return:
- `Result`
- `Created/Updated File`
- `Confirmed Facts And Constraints`
- `Open Questions`
- `Next Recommended Action`
- `Next Recommended Skill`
