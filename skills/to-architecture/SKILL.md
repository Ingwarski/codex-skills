---
name: to-architecture
description: Use when docs/prd.md exists and the user wants architecture.md, technical architecture, system architecture, module map, integration map, data/state model, runtime model, architectural decisions, risks, or architecture source-of-truth before DoD/evals, QA, or implementation planning.
---
# to-architecture

## Universal SDD Rule
AI is not the source of truth. Source files and explicit user answers are the source of truth. Mirror source terminology exactly; when sources use conflicting terms for one concept, do not pick silently - ask or flag it in `Open Questions`, then record the canonical term and aliases to avoid.

If blocker-level information is missing from the source files, do not create or update the output file yet. Use a focused grill-me gap-check first. Resolve the decision tree one branch at a time, ask one question at a time when the answer affects the next question, and include a recommended answer with each question. If the answer can be found by inspecting source files or the codebase, inspect instead of asking. Do not turn guesses into facts.

Create only the final output file. Do not write unverified assumptions into the artifact. Before creating or updating `docs/architecture.md`, every load-bearing architecture decision must be source-backed, user-confirmed, codebase-confirmed, or left in `Open Questions`.

If a gap-check ran, or if the skill synthesized architecture decisions not fully determined by source files or existing code, play back the resolved decisions to the user in a pithy summary and proceed only after confirmation. If sources and code already confirm this exact direction, create the artifact and surface the decisions in the Final Report.

## Input
Read:
- `README.md`, if present
- `docs/prd.md`
- `docs/user-journey.md`, if present
- `docs/screen-map.md`, if present
- `docs/wireframes.md`, if present
- `docs/ux-ui-brief.md`, if present
- `docs/guardrails.md`, if the user deliberately ran `to-guardrails` before this skill
- `docs/product-idea.md`, only if `docs/prd.md` explicitly names it as an authoritative source or the user asks to use it

Inspect the codebase structure when implementation will happen in an existing project. Existing code, package manifests, routes, schemas, environment files, and config files can confirm architecture facts; they do not authorize new product scope.

## Output
Create or update exactly one artifact:
- `docs/architecture.md`

Do not modify unrelated files.

## Artifact Boundary
`docs/architecture.md` owns:
- system architecture overview
- architecture principles and constraints
- module, service, route, and boundary map
- data and state model
- integration map
- runtime and automation model
- technology stack constraints when source-backed or codebase-confirmed
- security, privacy, reliability, performance, and observability architecture concerns
- architecture decision log with alternatives and consequences
- architecture risks and mitigations

It must not define:
- new product requirements
- user journey content
- screen inventory or state list
- wireframe layouts
- visual design direction
- Definition of Done, eval gates, or QA checklist items
- implementation units or task breakdown

Later artifacts may reference this file, but they must not duplicate its content.

## Proven Mechanics To Use
Adapt the useful parts of proven architecture/documentation skills without importing their bad fit:
- From `tad-generator`: extract PRD context first; clarify architecture only when source data is insufficient; cover system overview, architecture diagram, technology stack, system components, data architecture, infrastructure/runtime, security, performance/reliability, development constraints, and risks; validate that the diagram and sections are complete before reporting success.
- From `documentation-and-adrs`: document why, not only what; capture significant decisions, alternatives considered, rejection reasons, and consequences; preserve decision history instead of silently rewriting it.
- From `breakdown-epic-arch`: use a high-level architecture diagram and identify technical enablers, but do not hard-code any stack or epic path.
- From durable architecture-doc patterns: make the document useful for future agents so they do not re-derive architecture every session.
- From SDD guardrails: source docs and confirmed code win over assistant preference, generated mockups, or generic stack defaults.
- Static design artifacts can inform UI architecture boundaries, but they cannot prove runtime behavior, real state/data/actions, or completed functionality.

Do not copy these source skills wholesale:
- Do not write `tad.md`; write `docs/architecture.md`.
- Do not commit, push, update README indexes, or perform repo sync from inside the skill.
- Do not force startup cost estimates, specific hosted infrastructure, React/Next/tRPC, Docker, PostgreSQL, Redis, or any stack choice unless sources or code confirm them.
- Do not browse for "latest best stack" unless a named external platform, standard, or package version is required and likely current.

## Authoring References Used
These references were used to design this skill. They are not product source files for a project run; product truth still comes only from the Input files and explicit user answers.

- `tad-generator`: `https://github.com/luongnv89/skills/blob/main/skills/tad-generator/SKILL.md`
  - Used: PRD extraction, architecture clarification, system overview, Mermaid diagram, stack/components/data/infrastructure/security/performance/risk coverage, artifact acceptance checks.
  - Not used: `tad.md` output path, automatic git sync/commit/push, README index updates, startup cost defaults, and forced stack assumptions.
- `documentation-and-adrs`: `https://github.com/addyosmani/agent-skills/blob/main/skills/documentation-and-adrs/SKILL.md`
  - Used: document why, alternatives considered, decision consequences, ADR-style decision log.
  - Not used: separate ADR file workflow under `docs/decisions/`, because this skill creates one artifact only.
- `breakdown-epic-arch`: `https://github.com/github/awesome-copilot/blob/main/skills/breakdown-epic-arch/SKILL.md`
  - Used: high-level architecture specification shape, Mermaid architecture diagram, technical enabler thinking.
  - Not used: hard-coded TypeScript/Next.js/tRPC/Turborepo/Docker/Stack Auth assumptions and epic-specific output path.
- `eatmycode`: `https://github.com/xwings/eatmycode`
  - Used: durable architecture documentation as a future-agent alignment surface.
  - Not used: multi-file `ARCHITECTURE.md` plus `ARCHITECTURE/<module>.md` structure, because this pipeline uses one output artifact per skill.
- Existing local SDD skills in this repository:
  - `skills/to-guardrails/SKILL.md`
  - `skills/to-development-plan/SKILL.md`
  - Used: Universal SDD Rule, one-artifact output contract, artifact boundary format, source-backed/open-question behavior, and Final Report shape.

## Gap-Check
Before writing, verify that sources or code identify:
- product scope and architectural drivers
- target platform and runtime environment
- major modules, surfaces, services, or subsystems
- data/state objects and ownership
- external integrations and boundaries
- authentication, authorization, privacy, and security needs, if relevant
- performance, reliability, offline, observability, or scalability needs, if relevant
- deployment, hosting, repository, or automation constraints, if relevant
- architecture decisions that are already settled versus open

If stack, runtime, data ownership, integrations, security boundaries, or deployment constraints are missing and materially affect architecture, stop and ask grill-me questions before producing the output.

Ask architecture questions with recommended answers based on sources. Prefer:
- preserving existing codebase architecture
- using the simplest architecture that satisfies the PRD
- deferring unconfirmed infrastructure decisions to `Open Questions`
- using explicit interface boundaries before inventing services

## Workflow
1. Inspect the input files.
2. Inspect codebase structure when a codebase exists: package manifests, app routes, source directories, schemas, configs, tests, build scripts, and environment examples.
3. Extract architecture drivers from source artifacts: scope, users, screens, states, integrations, data, automation, constraints, and non-goals.
4. Identify existing architecture facts separately from proposed architecture decisions.
5. Define system context and module boundaries without adding product scope.
6. Define data/state ownership and flow.
7. Define integration and runtime/automation boundaries.
8. Define technology constraints only where source-backed or codebase-confirmed.
9. Capture important decisions with alternatives and consequences.
10. Include an architecture diagram when it clarifies the system. Use Mermaid and keep it readable.
11. Before writing the artifact, verify the planned content:
   - Every load-bearing architecture decision traces to a named source file, codebase evidence, or an explicit user answer, or it is moved to `Open Questions`.
   - No content belongs to another artifact's ownership per the Artifact Boundary.
   - No placeholder text and no generic filler written to satisfy the template.
   - The architecture does not invent product scope, screens, features, or implementation tasks.
12. Create or update only `docs/architecture.md`.

## Required Output Structure
Use this structure:

Required contract sections are `Source References`, `Architecture Overview`, `Architecture Principles`, `Module And Boundary Map`, `Data And State Model`, `Integration Map`, `Architecture Decision Log`, `Risks And Mitigations`, `Out Of Scope`, and `Open Questions`. Optional sections may be omitted when sources give them no content. Required sections may use a single line `Not applicable: <reason>` only when the reason is source-backed. Never fill a section to satisfy the template. List omitted optional sections in the Final Report.

```markdown
# Architecture

## Source References

## Architecture Overview

## Architecture Principles

## System Context

## Module And Boundary Map

## Runtime And Automation Model

## Data And State Model

## Integration Map

## Technology Stack And Constraints

## Security Privacy And Access Model

## Performance Reliability And Observability

## Architecture Diagram

## Architecture Decision Log

## Risks And Mitigations

## Out Of Scope

## Open Questions
```

For each important architecture decision include:
- `Decision`
- `Source References`
- `Alternatives Considered`
- `Why This Direction`
- `Consequences`
- `Open Follow-Up`, if any

## Final Report
Return:
- `Result`
- `Created/Updated File`
- `Confirmed Architecture Facts And Constraints`
- `Omitted Optional Sections`, if any
- `Open Questions`
- `Next Recommended Action`
- `Next Recommended Skill`
