---
name: to-ux-ui-brief
description: Use when docs/wireframes.md exists and the user wants the UX/UI brief, design direction, visual system, design tokens, typography and color direction, interaction rules, or design handoff.
---
# to-ux-ui-brief

## Universal SDD Rule
AI is not the source of truth. Source files and explicit user answers are the source of truth. Mirror source terminology exactly; when sources use conflicting terms for one concept, do not pick silently - ask or flag it in `Open Questions`, then record the canonical term and aliases to avoid.

If blocker-level information is missing from the source files, do not create or update the output file yet. Use a focused grill-me gap-check first. Resolve the decision tree one branch at a time, ask one question at a time when the answer affects the next question, and include a recommended answer with each question. If the answer can be found by inspecting source files or the codebase, inspect instead of asking. Do not turn guesses into facts.

For aesthetic direction, the assistant may propose 2-3 clearly labeled options during gap-check, but the final brief must use only a direction supported by source files or explicitly selected by the user.

Create only the final output file. Do not write unverified assumptions into the artifact. Before creating or updating `docs/ux-ui-brief.md`, every load-bearing claim must be source-backed, user-confirmed, or left in `Open Questions`.

If a gap-check ran, or if the skill synthesized decisions not fully determined by source files, play back the resolved decisions to the user in a pithy summary and proceed only after confirmation. If sources already confirm this exact direction, create the artifact and surface the decisions in the Final Report. For this skill, UX/UI direction is usually synthesis, so playback is expected unless the exact visual direction was already confirmed.

## Input
Read:
- `README.md`, if present
- `docs/prd.md`
- `docs/user-journey.md`
- `docs/screen-map.md`
- `docs/wireframes.md`
- `docs/guardrails.md`, if the user deliberately ran `to-guardrails` before this skill

## Output
Create or update exactly one artifact:
- `docs/ux-ui-brief.md`

Do not modify unrelated files.

## Artifact Boundary
`docs/ux-ui-brief.md` owns:
- UX/UI design intent
- visual direction
- design brief
- design decision log
- information density and interface tone
- semantic design tokens
- typography direction
- color direction
- spacing and layout rhythm
- component appearance principles
- interaction feel
- responsive behavior
- accessibility floor
- design handoff guidance

For states: `docs/screen-map.md` owns which states exist per screen; `docs/wireframes.md` owns each state's structure; this file owns system-wide state appearance and behavior patterns. Reference the screen-map state list; do not re-derive it.

It must not define:
- new product features
- new screens or routes
- detailed wireframe structure already owned by `docs/wireframes.md`
- QA checklist items
- implementation tasks

Reference prior artifacts instead of restating them.

## Proven Mechanics To Use
Adapt the strongest UX Coach mechanics into a single SDD artifact:
- Treat the brief as two spines inside one file: `Design Spine` and `Experience Spine`.
- The Design Spine is the visual contract: brand/style, colors, typography, spacing, radius, elevation, component appearance, visual do/don't rules.
- The Experience Spine is the behavior contract: form factor, IA implications, voice/tone rules, component behavior, state patterns, interaction primitives, accessibility, key flows.
- Spines win over mockups. Wireframes, screenshots, Stitch output, v0 output, or Figma explorations are illustrations, not the source of truth.
- Keep a `Decision Log` for selected directions, rejected directions, scope cuts, tool choices, and user overrides.
- Run a concern scan: accessibility, platform conventions, brand voice, regulated language, motion, internationalization, dark mode, offline behavior, content density, input modalities, notifications, AI control and reversibility.
- Surface UI system inheritance. If shadcn, MUI, Tailwind, native UIKit, Compose, or an internal design system exists, extend or reference it instead of inventing a parallel system.
- Use visual-first structures where useful: token tables, state matrices, component spec tables, Mermaid flow diagrams, and small swatch/type/spacing examples.
- When current UI systems, accessibility standards, platform HIGs, or named visual references may have changed, verify them with current sources before creating or updating the artifact.

Use the strongest production UX/UI mechanics:
- Start from user goal, audience, primary action, and product context.
- Match experience type: SaaS/operational tool, checkout, AI product, course/content, dashboard, landing/sales, mobile app, internal tool, or regulated workflow.
- Preserve existing design systems unless the user explicitly wants a redesign.
- Define complete states: default, hover, focus, active, disabled, loading, empty, error, success, long-content, offline, and permission-denied when relevant.
- Meet WCAG 2.2 AA by default: contrast, visible focus, keyboard access, semantic structure, labels, errors, target sizes, and reduced-motion support.
- When project principles or user policy define font constraints, verify font licensing and provenance before selection. If provenance cannot be confidently verified, prefer system stacks or verified independent foundries.
- Plan responsive behavior at 390, 430, 768, 1280, and 1440px unless sources specify different target devices.
- Avoid one-note palettes, decorative blobs, meaningless gradients, hidden scrollbars, card-in-card layouts, and visual trend choices that weaken usability.

## Gap-Check
Before writing, verify that sources identify:
- target audience and product category
- brand or desired product feeling
- platform and device priorities
- complexity and information-density needs
- accessibility expectations
- visual constraints, if any
- existing design system, visual source, brand deck, screenshots, tokens, component library, or inspiration/rejection references
- expected interactivity and motion level
- whether the user wants a fast path with explicit assumptions or a coached path with decisions resolved section by section

If visual direction, audience, density, or platform priorities are missing or contradictory, stop and ask grill-me questions before producing the output.

## Workflow
1. Inspect the input files.
2. Find grounding material before inventing: design docs, screenshots, Figma links, Storybook, tokens, components, CSS variables, brand assets, or reference products named by the user.
3. Extract UX intent from the PRD, user journey, screen map, and wireframes.
4. Identify the product type, stakes, form factor, and level of visual sophistication needed.
5. Run the concern scan and decide which concerns deserve sections.
6. Define a source-backed Design Spine.
7. Define a source-backed Experience Spine.
8. Critique the planned Design Spine against generic AI defaults: templated palettes, interchangeable type pairings, decorative filler, and styles that could belong to any product in the category. Name one signature element or one deliberate restraint principle grounded in the product's domain, and state where the design spends or withholds boldness. If the direction is not product-specific, revise it or raise clearly labeled aesthetic options for the user to select.
9. Define semantic tokens and component appearance principles without overbuilding a design-system monster.
10. Define responsive, accessibility, state, and interaction expectations.
11. Add handoff prompts or guidance for Figma, v0, Stitch, or Codex only when useful and only from captured content.
12. Run the Validation Pass defined below before creating or updating the artifact.
13. Avoid changing scope, adding screens, or rewriting wireframes.
14. Before writing the artifact, verify the planned content:
   - Every load-bearing claim traces to a named source file or an explicit user answer, or it is moved to `Open Questions`.
   - No content belongs to another artifact's ownership per the Artifact Boundary.
   - No placeholder text and no generic filler written to satisfy the template.
15. Create or update only `docs/ux-ui-brief.md`.

## Validation Pass
Run both passes on the planned artifact content. Record results in the artifact's `Validation Report` as findings ranked by downstream impact: Critical, High, Medium, Low. If a pass has no findings, state `0 findings` for that pass.

Pass 1 - Mechanical coverage:
- Every key flow referenced names its journey source and has success and failure coverage in the Experience Spine.
- Every token referenced anywhere in the brief resolves to a defined value in the Design Spine.
- Every component named in either spine has both an appearance principle and a behavior principle.
- Every screen and state in `docs/screen-map.md` is covered by a state pattern or explicitly deferred with a reason.
- Every visual reference, link, or source named in the brief resolves; unavailable sources are flagged, never silently dropped.

Pass 2 - Judgment:
- Bloat: no pixel specs where tokens suffice, no decorative prose, no sections filled to satisfy the template.
- Inheritance: named UI systems, versions, and source terminology are used faithfully; no parallel system is invented.
- Shape: sections follow the required structure; spines stay contracts, not restated wireframes.

## Required Output Structure
Use this structure:

Required contract sections are `Source References`, `Design Brief`, `Decision Log`, `Product Experience Goal`, `Design Spine`, `Experience Spine`, `Validation Report`, and `Open Questions`. Optional sections may be omitted when sources give them no content. Required sections may use a single line `Not applicable: <reason>` only when the reason is source-backed. Never fill a section to satisfy the template. List omitted optional sections in the Final Report.

```markdown
# UX/UI Brief

## Source References

## Design Brief

## Decision Log

## Audience And Context

## Product Experience Goal

## Concern Scan

## Design Spine

Token values live only in `### Design Tokens`; other spine sections reference tokens by name instead of repeating values.

### Brand And Style

### Colors

### Typography

### Layout And Spacing

### Elevation And Depth

### Shapes

### Component Appearance

### Visual Do's And Don'ts

### Design Tokens

## Experience Spine

### Foundation

### Information Architecture Implications

### Voice And Tone

### Component Behavior

### State Patterns

### Interaction Primitives

### Accessibility Floor

### Key Flow Implications

## Responsive And Platform Behavior

## Design Handoff Prompt

## Validation Report

## Confirmed Design Decisions

## Rejected Directions

## Out Of Scope

## Open Questions
```

## Final Report
Return:
- `Result`
- `Created/Updated File`
- `Confirmed Design Decisions`
- `Omitted Optional Sections`, if any
- `Open Questions`
- `Next Recommended Action`
- `Next Recommended Skill`
