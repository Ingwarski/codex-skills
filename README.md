# Codex SDD Skills

This repository contains a small chain of Codex skills for moving from a PRD to product UX/UI planning and implementation planning.

The skills are designed for **SDD - Specification Driven Development**. They are not a TDD workflow and they are not generic prompt templates. Each skill creates exactly one artifact, uses source files as the source of truth, and asks focused questions before writing when critical information is missing.

## Skill Chain

Use the skills in this order:

```text
to-prd
-> to-user-journey
-> to-screen-map
-> to-wireframes
-> to-ux-ui-brief
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
| `to-ux-ui-brief` | `docs/ux-ui-brief.md` | Defines the UX/UI direction, Design Spine, Experience Spine, visual system, interaction rules, responsive behavior, accessibility floor, and design handoff guidance. |
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
- `ux-ui-brief.md` owns visual and experience direction.
- `guardrails.md` owns AI behavior and source-of-truth policy.
- `qa-checklist.md` owns verification checks and evidence artifacts.
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
ln -s "/Users/ingwar/Documents/Codex Skills/skills/to-ux-ui-brief" ~/.codex/skills/to-ux-ui-brief
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
Use to-ux-ui-brief for this project.
Use to-guardrails for this project.
Use to-qa-checklist for this project.
Use to-development-plan for this project.
```

`to-guardrails` can also be run earlier, any time after `docs/prd.md` exists. Running it before design artifacts is useful when you want the whole pipeline constrained by explicit AI behavior rules. Re-run it later after UX artifacts exist if design-authority rules need to be added.

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
- a Design Spine and Experience Spine in `ux-ui-brief.md`;
- visual-system inheritance when a project already has tokens, components, or a design system;
- accessibility and responsive behavior as default requirements;
- validation before the UX/UI brief is written;
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

## Repository Contents

```text
skills/
  to-user-journey/
    SKILL.md
  to-screen-map/
    SKILL.md
  to-wireframes/
    SKILL.md
  to-ux-ui-brief/
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
