---
name: to-dod-evals
description: Use when approved SDD product and architecture artifacts exist and the user wants dod-evals.md, Definition of Done, eval gates, verification profile, quality gates, lane/state promotion gates, PR/merge rules, or evidence requirements before QA checklist or development planning.
---
# to-dod-evals

## Universal SDD Rule
AI is not the source of truth. Source files and explicit user answers are the source of truth. Mirror source terminology exactly; when sources use conflicting terms for one concept, do not pick silently - ask or flag it in `Open Questions`, then record the canonical term and aliases to avoid.

If blocker-level information is missing from the source files, do not create or update the output file yet. Use a focused grill-me gap-check first. Resolve the decision tree one branch at a time, ask one question at a time when the answer affects the next question, and include a recommended answer with each question. If the answer can be found by inspecting source files or the codebase, inspect instead of asking. Do not turn guesses into facts.

Create only the final output file. Do not write unverified assumptions into the artifact. Before creating or updating `docs/dod-evals.md`, every DoD rule, gate, eval, and evidence requirement must be source-backed, user-confirmed, codebase-confirmed, or left in `Open Questions`.

If a gap-check ran, or if the skill synthesized verification rules not fully determined by source files or existing code, play back the resolved decisions to the user in a pithy summary and proceed only after confirmation. If sources and code already confirm this exact direction, create the artifact and surface the decisions in the Final Report.

## Input
Read:
- `README.md`, if present
- `docs/prd.md`
- `docs/user-journey.md`, if present
- `docs/screen-map.md`, if present
- `docs/wireframes.md`, if present
- `docs/design-brief.md`, if present
- `docs/architecture.md`
- `docs/guardrails.md`, if the user deliberately ran `to-guardrails` before this skill
- `docs/product-idea.md`, only if `docs/prd.md` explicitly names it as an authoritative source or the user asks to use it

Inspect the codebase when implementation or verification will happen in an existing project. Package scripts, CI config, tests, build config, lint/typecheck config, and deployment config can confirm available gates; they do not authorize new product scope.

## Output
Create or update exactly one artifact:
- `docs/dod-evals.md`

Do not modify unrelated files.

## Artifact Boundary
`docs/dod-evals.md` owns:
- Definition of Done model
- distinction between acceptance criteria and standing DoD
- reusable verification profile
- hard gates, unit checks, system checks, UX/UI checks, and release gates
- lane/state promotion gates when the product has workflow states
- eval result format
- completion evidence requirements
- failure and blocker classification
- rerun, recovery, PR, merge, and completion rules

It must not define:
- new product requirements
- architecture decisions
- user journeys
- screen inventory or wireframe layouts
- visual design direction
- per-screen QA checklist details
- implementation units or task breakdown

`docs/guardrails.md` owns the behavioral evidence policy: when the AI must verify, what counts as evidence, and when missing evidence must stop work. `docs/dod-evals.md` uses that policy to define the reusable completion/eval contract and gate-specific evidence required for Done. `docs/qa-checklist.md` owns concrete checklist items and per-check evidence artifacts for a specific product artifact or release.

## Proven Mechanics To Use
Adapt the useful parts of proven DoD, quality-gate, planning, and eval references:
- From `definition-of-done`: separate acceptance criteria from Definition of Done; acceptance asks "did we build the right thing"; DoD asks "is it finished to our standard"; use a stable reusable bar for correctness, quality, integration, documentation, and ship-readiness.
- From `quality-run-quality-gates`: detect available project gates; run gates before completion claims; report pass/fail clearly; completion is blocked until gates pass; rerun after fixes.
- From `verification-before-completion`: evidence before claims; identify what proves the claim, run it fresh, read the output, then state the result.
- From `breakdown-plan`: define DoD at useful levels such as product, feature/unit, story/task, enabler, and test where sources support those levels.
- From eval/lane-gate patterns: attach eval definitions to workflow state transitions; a lane promotion is blocked until required evals pass; evals have standard result shape and persistable evidence.
- From SDD guardrails: source docs and confirmed code win over agent self-assessment.
- Treat mockups, screenshots, prototypes, and visually convincing static surfaces as design/visual evidence only. They do not prove completed functionality unless connected to source-backed behavior, real state/data/actions, runner evidence, and required DoD gates.

Do not copy these source skills wholesale:
- Do not turn this into a command runner. This skill writes the DoD/evals source-of-truth document; it does not execute gates.
- Do not create GitHub issues, project automation, or sprint plans.
- Do not equate "tests pass" with done.
- Do not claim WCAG, security, performance, or compliance guarantees from static docs alone.
- Do not invent CI scripts, package scripts, eval harnesses, PR rules, or deployment gates when sources or code do not support them.

## Authoring References Used
These references were used to design this skill. They are not product source files for a project run; product truth still comes only from the Input files and explicit user answers.

- `definition-of-done`: `https://raw.githubusercontent.com/addyosmani/agent-skills/main/references/definition-of-done.md`
  - Used: acceptance criteria vs Definition of Done distinction, standing reusable DoD, correctness/quality/integration/documentation/ship-readiness sections, and red flags against declaring done too early.
  - Not used: one-size-fits-all checklist as final content; project-specific source files still decide what belongs in `docs/dod-evals.md`.
- `quality-run-quality-gates`: `https://github.com/dawiddutoit/custom-claude/blob/main/skills/quality-run-quality-gates/SKILL.md`
  - Used: gate detection mindset, pass/fail reporting, rerun-after-fix loop, and "Definition of Done met/not met" blocking semantics.
  - Not used: command-runner behavior, tool-specific scripts, or executing gates during artifact creation.
- `verification-before-completion`: `/Users/ingwar/.codex/plugins/cache/openai-curated/superpowers/d6169bef/skills/verification-before-completion/SKILL.md`
  - Used: evidence before claims, identify/run/read/verify gate function, no completion claim without fresh evidence.
  - Not used: runtime execution as the artifact output; this skill writes the reusable DoD/eval contract.
- `breakdown-plan`: `https://github.com/github/awesome-copilot/blob/main/skills/breakdown-plan/SKILL.md`
  - Used: DoD at multiple planning levels, acceptance criteria plus Definition of Done, dependency and gate thinking.
  - Not used: GitHub project automation, issue hierarchy output, sprint/project-management artifacts.
- Hermes eval/lane-gate proposal: `https://github.com/NousResearch/hermes-agent/issues/44000`
  - Used: eval definitions attached to lane/state transitions, standard eval result shape, quality contract over agent self-assessment.
  - Not used: Hermes-specific architecture, cron/memory/CLI implementation proposals.
- Existing local SDD skills in this repository:
  - `skills/to-guardrails/SKILL.md`
  - `skills/to-qa-checklist/SKILL.md`
  - `skills/to-development-plan/SKILL.md`
  - Used: Universal SDD Rule, one-artifact output contract, evidence policy separation, artifact boundaries, severity/release-readiness separation, and Final Report shape.

## Gap-Check
Before writing, verify that sources or code identify:
- product acceptance criteria or success conditions
- architecture/runtime constraints that affect verification
- workflow states, lanes, or completion transitions
- required hard gates such as build, lint, typecheck, tests, security scan, or manual approval
- UX/UI verification expectations
- PR, merge, branch, commit, or release rules, if relevant
- what evidence counts for completion claims
- whether UI/design evidence is connected to real behavior, state, data, and actions when functionality is claimed
- failure classes and blocker handling
- which checks can be automated now versus later

If verification profile, completion gates, workflow promotion rules, or merge/completion rules are missing and materially affect the document, stop and ask grill-me questions before producing the output.

Ask DoD/eval questions with recommended answers based on sources. Prefer:
- `passed` only when required gates pass with fresh evidence
- `blocked` when P0/P1/P2 or required gates remain open
- static docs can define intended checks but cannot prove runtime behavior
- manual approval is required for user-facing or irreversible transitions unless sources say otherwise

## Workflow
1. Inspect the input files.
2. Inspect codebase verification surfaces when a codebase exists: `package.json`, test directories, CI config, lint/typecheck config, build scripts, Playwright/Vitest/Jest config, and deployment config.
3. Extract acceptance criteria and completion semantics from the PRD and related SDD artifacts.
4. Extract architecture-driven verification needs from `docs/architecture.md`.
5. Separate acceptance criteria, DoD, QA checklist items, and implementation tasks.
6. Define the standing DoD model.
7. Define verification profile tiers: hard gates, unit checks, system checks, UX/UI checks, evidence, static-surface limits, and release/merge checks.
8. Define lane/state promotion gates when the product has workflow states or Kanban-like transitions.
9. Define eval result format with pass/fail/blocked status, evidence, owner, timestamp/source, and rerun rule.
10. Define failure and blocker classification without duplicating `docs/qa-checklist.md`.
11. Before writing the artifact, verify the planned content:
   - Every DoD rule, gate, eval, and evidence requirement traces to a named source file, codebase evidence, or explicit user answer, or it is moved to `Open Questions`.
   - No content belongs to another artifact's ownership per the Artifact Boundary.
   - No placeholder text and no generic filler written to satisfy the template.
   - The artifact does not invent tests, scripts, CI, PR policy, or implementation scope.
12. Create or update only `docs/dod-evals.md`.

## Required Output Structure
Use this structure:

Required contract sections are `Source References`, `Definition Of Done Model`, `Verification Profile`, `Gate Matrix`, `Evidence Requirements`, `Failure And Blocker Classification`, `PR Merge And Completion Rules`, `Out Of Scope`, and `Open Questions`. Optional sections may be omitted when sources give them no content. Required sections may use a single line `Not applicable: <reason>` only when the reason is source-backed. Never fill a section to satisfy the template. List omitted optional sections in the Final Report.

```markdown
# DoD And Evals

## Source References

## Definition Of Done Model

## Acceptance Criteria Vs Definition Of Done

## Global Definition Of Done

## Feature Unit Definition Of Done

## Verification Profile

### Hard Gates

### Unit Checks

### System Checks

### UX/UI Checks

### Release Checks

## Gate Matrix

## Lane Or State Promotion Gates

## Eval Result Format

## Evidence Requirements

## Evidence Limits

## Failure And Blocker Classification

## Rerun And Recovery Rules

## PR Merge And Completion Rules

## Out Of Scope

## Open Questions
```

For every gate or eval include:
- `Gate`
- `Purpose`
- `Source References`
- `Applies To`
- `Required Evidence`
- `Pass Condition`
- `Fail Or Block Condition`
- `Rerun Rule`
- `Automation Status`: `automated`, `manual`, `not available yet`, or `open question`

## Final Report
Return:
- `Result`
- `Created/Updated File`
- `Confirmed DoD And Eval Rules`
- `Omitted Optional Sections`, if any
- `Open Questions`
- `Next Recommended Action`
- `Next Recommended Skill`
