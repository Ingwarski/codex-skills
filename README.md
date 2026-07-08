# Codex SDD Skills

This repository contains a small chain of Codex skills for moving from a PRD to product UX/UI planning, architecture, DoD/evals, QA, and implementation planning.

The skills are designed for **SDD - Specification Driven Development**. They are not a TDD workflow and they are not generic prompt templates. Each skill creates exactly one artifact, uses source files as the source of truth, and asks focused questions before writing when critical information is missing.

## Skill Chain

Use the skills in this order:

```text
to-prd
-> to-user-journey
-> to-screen-map
-> to-wireframes
-> to-design-brief
-> to-architecture
-> to-dod-evals
-> to-guardrails
-> to-qa-checklist
-> to-development-plan
```

`to-prd` is not included in this repository. These skills start after `docs/prd.md` exists.

## Included Skills

| Skill | Output | Purpose |
|---|---|---|
| `to-user-journey` | `docs/user-journey.md` | Maps the real user, goal, context, journey stages, friction, decisions, failure path, and success state. |
| `to-screen-map` | `docs/screen-map.md` | Defines screens, surfaces, routes, navigation, transitions, entry/exit points, and the canonical state list per screen. |
| `to-wireframes` | `docs/wireframes.md` | Converts the screen map into low-fidelity screen structures, hierarchy, CTAs, forms, content zones, and state variants. |
| `to-design-brief` | `docs/design-brief.md` | Defines the UX/UI direction, Design Spine, Experience Spine, visual system, interaction rules, responsive behavior, accessibility floor, and design handoff guidance. |
| `to-architecture` | `docs/architecture.md` | Defines system architecture, modules, boundaries, data/state model, integrations, runtime model, architecture decisions, and risks. |
| `to-dod-evals` | `docs/dod-evals.md` | Defines Definition of Done, reusable eval gates, verification profile, evidence requirements, state/lane gates, and PR/merge completion rules. |
| `to-guardrails` | `docs/guardrails.md` | Defines source-of-truth order, AI autonomy boundaries, scope limits, conflict handling, stop conditions, and verification policy. |
| `to-qa-checklist` | `docs/qa-checklist.md` | Creates a source-backed QA checklist with acceptance, UX/UI, responsive, accessibility, visual regression, evidence, and release-readiness checks. |
| `to-development-plan` | `docs/development-plan.md` | Converts approved SDD artifacts into implementation units, dependency order, acceptance checks, and verification steps. |

## Core Rules

All skills follow the same operating contract:

- AI is not the source of truth. Source files and explicit user answers are.
- If critical information is missing, the skill must run a focused grill-me gap-check before writing the output artifact.
- The skill creates only the final output file. No draft output files.
- Unverified assumptions are not written into artifacts.
- Anything not source-backed or user-confirmed goes to `Open Questions`.
- Each skill creates or updates exactly one artifact.
- Artifacts reference prior artifacts instead of duplicating them.
- Artifact boundaries must be preserved.

## Artifact Boundaries

The documents are intentionally separated:

- `user-journey.md` owns user behavior and journey logic.
- `screen-map.md` owns which screens and states exist.
- `wireframes.md` owns screen structure and state structure.
- `design-brief.md` owns visual and experience direction.
- `architecture.md` owns system architecture, module boundaries, data/state model, integrations, runtime model, and architecture decisions.
- `dod-evals.md` owns Definition of Done, reusable gates, eval result format, completion evidence requirements, and completion rules.
- `guardrails.md` owns AI behavior, source-of-truth policy, and behavioral evidence policy.
- `qa-checklist.md` owns concrete verification checks and per-check evidence artifacts.
- `development-plan.md` owns implementation units and build order.

If one artifact needs information from another, it should cite or reference that artifact rather than restating it.

## Installation

For Codex to discover these skills, place each skill directory under your Codex skills directory.

Recommended local install with symlinks:

```bash
mkdir -p ~/.codex/skills
ln -s "/Users/ingwar/Documents/Codex Skills/skills/to-user-journey" ~/.codex/skills/to-user-journey
ln -s "/Users/ingwar/Documents/Codex Skills/skills/to-screen-map" ~/.codex/skills/to-screen-map
ln -s "/Users/ingwar/Documents/Codex Skills/skills/to-wireframes" ~/.codex/skills/to-wireframes
ln -s "/Users/ingwar/Documents/Codex Skills/skills/to-design-brief" ~/.codex/skills/to-design-brief
ln -s "/Users/ingwar/Documents/Codex Skills/skills/to-architecture" ~/.codex/skills/to-architecture
ln -s "/Users/ingwar/Documents/Codex Skills/skills/to-dod-evals" ~/.codex/skills/to-dod-evals
ln -s "/Users/ingwar/Documents/Codex Skills/skills/to-guardrails" ~/.codex/skills/to-guardrails
ln -s "/Users/ingwar/Documents/Codex Skills/skills/to-qa-checklist" ~/.codex/skills/to-qa-checklist
ln -s "/Users/ingwar/Documents/Codex Skills/skills/to-development-plan" ~/.codex/skills/to-development-plan
```

If a symlink already exists, remove or update only that symlink. Do not overwrite an existing personal skill with the same name unless that is intentional.

## How To Use

Start in a product project that has at least:

```text
docs/prd.md
```

Useful optional project context:

```text
README.md
```

Do not create extra context documents just to satisfy this pipeline. The skills should use `docs/prd.md`, the relevant earlier pipeline artifacts, and explicit user answers as the source of truth. `docs/guardrails.md` is not a starting input; it is created by `to-guardrails` and can only be used by later skills or by earlier skills if the user deliberately ran guardrails first.

Then ask Codex to run each skill in sequence.

Example:

```text
Use to-user-journey for this project.
```

Then:

```text
Use to-screen-map for this project.
Use to-wireframes for this project.
Use to-design-brief for this project.
Use to-architecture for this project.
Use to-dod-evals for this project.
Use to-guardrails for this project.
Use to-qa-checklist for this project.
Use to-development-plan for this project.
```

`to-guardrails` can also be run earlier, any time after `docs/prd.md` exists. Running it before design artifacts is useful when you want the whole pipeline constrained by explicit AI behavior rules. Re-run it later after UX artifacts exist if design-authority rules need to be added.

`to-architecture` and `to-dod-evals` should run before `to-qa-checklist` and `to-development-plan` when the product needs architecture and completion gates as source-of-truth documents. `to-dod-evals` requires an approved `docs/architecture.md`; if a tiny project does not need separate architecture or completion artifacts, skip both and keep that decision explicit in downstream `Open Questions`. `to-qa-checklist` verifies those contracts; it does not replace them.

Keep the chain skippable rather than ceremonial for tiny projects: run optional artifacts only when their owned decisions are needed as source truth.

## What Happens When Information Is Missing

The skills should not invent missing product decisions.

When a blocker-level gap exists, the skill should stop before writing the output file and ask focused questions. The question style follows a grill-me pattern:

- ask one question at a time when the answer affects the next question;
- include a recommended answer;
- inspect source files or the codebase instead of asking when the answer can be found there;
- continue only after the missing decision is resolved.

If the gap is not blocking, the skill should write the artifact and list the unresolved item in `Open Questions`.

## Design Quality

The UX/UI part of the chain is built around proven product-design mechanisms:

- real user journeys instead of feature lists;
- surface closure between journeys and screens;
- concrete wireframe notation rather than vague layout prose;
- a Design Spine and Experience Spine in `design-brief.md`;
- visual-system inheritance when a project already has tokens, components, or a design system;
- accessibility and responsive behavior as default requirements;
- validation before the design brief is written;
- a distinctiveness check so the design does not collapse into generic AI UI.

For operational products, a deliberate restraint principle can be the right design decision. The skills should not force decorative design when the product needs density, clarity, and repeat-use efficiency.

## QA And Implementation

`to-qa-checklist` produces checks with severity:

- `P0`: blocks core use or is a severe accessibility failure.
- `P1`: major mismatch or usability regression.
- `P2`: moderate drift or fixable gap.
- `P3`: polish.

Release readiness is binary:

- `passed` only when no P0-P2 items remain open.
- `blocked` when P0-P2 blockers remain.

`to-development-plan` is SDD-first. Tests and verification support the approved spec, but they do not become the source of product truth.

`to-dod-evals` separates acceptance criteria from Definition of Done. Acceptance criteria confirm that a specific item was built correctly; DoD/eval gates define the standing completion bar and evidence required before anything can be called done. A mockup, screenshot, prototype, or visually convincing static surface is design/visual evidence only; it is not completed functionality unless connected to source-backed behavior, real state/data/actions, runner evidence, and required DoD gates.

## Authoring References

The skills are custom SDD skills, but they intentionally reuse proven mechanisms from existing skills and references.

For `to-architecture`, the main authoring references were:

- `tad-generator`: `https://github.com/luongnv89/skills/blob/main/skills/tad-generator/SKILL.md`
- `documentation-and-adrs`: `https://github.com/addyosmani/agent-skills/blob/main/skills/documentation-and-adrs/SKILL.md`
- `breakdown-epic-arch`: `https://github.com/github/awesome-copilot/blob/main/skills/breakdown-epic-arch/SKILL.md`
- `eatmycode`: `https://github.com/xwings/eatmycode`

For `to-dod-evals`, the main authoring references were:

- `definition-of-done`: `https://raw.githubusercontent.com/addyosmani/agent-skills/main/references/definition-of-done.md`
- `quality-run-quality-gates`: `https://github.com/dawiddutoit/custom-claude/blob/main/skills/quality-run-quality-gates/SKILL.md`
- `verification-before-completion`: `/Users/ingwar/.codex/plugins/cache/openai-curated/superpowers/d6169bef/skills/verification-before-completion/SKILL.md`
- `breakdown-plan`: `https://github.com/github/awesome-copilot/blob/main/skills/breakdown-plan/SKILL.md`
- Hermes eval/lane-gate proposal: `https://github.com/NousResearch/hermes-agent/issues/44000`

These references are authoring provenance, not product source files. During a project run, each skill must still use only its declared input files and explicit user answers as product truth.

## Repository Contents

```text
skills/
  to-user-journey/
    SKILL.md
  to-screen-map/
    SKILL.md
  to-wireframes/
    SKILL.md
  to-design-brief/
    SKILL.md
  to-architecture/
    SKILL.md
  to-dod-evals/
    SKILL.md
  to-guardrails/
    SKILL.md
  to-qa-checklist/
    SKILL.md
  to-development-plan/
    SKILL.md

claude-code-skill-audit-prompt.md
```

`claude-code-skill-audit-prompt.md` is the audit prompt used to review these skills against the user's requirements and relevant external skills.
