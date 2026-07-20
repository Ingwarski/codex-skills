---
name: to-sdd-pipeline
description: Orchestrate a design-first SDD pipeline from docs/product-idea.md through the coherent pre-design SDD baseline, exactly three runnable prototype candidates, one whole-design approval, post-approval reconciliation, and docs/development-plan.md. Use when the user wants the full SDD set generated or reconciled autonomously rather than invoking one artifact skill at a time.
---
# to-sdd-pipeline

## Mission

Run the SDD workflow as one autonomous dependency graph while preserving exclusive artifact ownership. The process exists to reduce an engineer's coordination work. Do not add file-by-file, screen-by-screen, or step-by-step approval gates.

## Input

Require:
- `docs/product-idea.md`
- the artifact-owner skills listed below
- a project-supported prototype producer or Product Design adapter before the prototype node runs

Read existing SDD artifacts and `forge/sdd-manifest.json` when present. Inspect the codebase for source-backed architecture, design-system, runtime, and verification facts instead of asking for discoverable information.

## Output And Ownership

This orchestrator directly creates or updates exactly one file:
- `forge/sdd-manifest.json`

It must never directly create or edit a domain artifact. Invoke or re-invoke the owning skill:

| Artifact | Owner |
|---|---|
| `docs/prd.md` | `to-prd` |
| `docs/guardrails.md` | `to-guardrails` |
| `docs/user-journey.md` | `to-user-journey` |
| `docs/screen-map.md` | `to-screen-map` |
| `docs/wireframes.md` | `to-wireframes` |
| `docs/design-brief.md` | `to-design-brief` |
| `docs/architecture.md` | `to-architecture` |
| `docs/dod-evals.md` | `to-dod-evals` |
| `docs/qa-checklist.md` | `to-qa-checklist` |
| `docs/development-plan.md` | `to-development-plan` |

An owner skill may change only its declared artifact. The orchestrator validates owner output, records its hash and provenance, then dispatches every newly ready node without asking the user to continue.

The prototype producer is a runtime adapter, not an SDD artifact owner. During Phase 2 it may write candidate-specific code/assets only under `forge/design/candidates/{candidate_id}/{version}/`, optional shared preview infrastructure only under the versioned `forge/design/candidate-sets/{candidate_set_id}/{set_version}/shared/` workspace, and normalized evidence under `forge/design/evidence/`. Shared runtime reuse resolves to that candidate-set version and cannot hide mutable source elsewhere. It must not write production application source directories, domain SDD artifacts, or the orchestration manifest. Every write records adapter, candidate/version or candidate-set version, target hash, and changed paths. Phase 3 implementation agents own production-code writes under the bounds of the approved development plan.

## Dependency Graph

Use this acyclic graph:

```text
product-idea
-> prd
-> guardrails
-> user-journey
-> screen-map
-> wireframes
-> design-brief
-> architecture
-> dod-evals
-> qa-checklist-proposed
-> coherent-pre-design-sdd
-> prototype-candidates
-> awaiting-design-approval
-> approved-visual-baseline
-> qa-checklist-approved
-> development-plan
```

`docs/guardrails.md` depends only on the PRD and explicitly authoritative upstream intent; it never reads downstream artifacts back into itself. `docs/wireframes.md` never depends on `docs/design-brief.md`. `docs/development-plan.md` never belongs to the pre-design baseline because it requires the Approved Visual Baseline.

Run independent ready nodes in parallel when their owner skills and workspace safety allow it. Serialize nodes that share a source file being updated.

## Autonomy And Stop Rules

Resolve non-material uncertainty from source files, codebase evidence, or the smallest reversible source-grounded default. Record the decision and continue.

Pause only for:
1. a genuinely non-inferable decision that materially changes product scope;
2. the engineer's one approval of the complete integrated prototype, which also selects the candidate and creates the Approved Visual Baseline;
3. just-in-time authorization before an irreversible, destructive, financial, legal, public, privileged, security-sensitive, privacy-sensitive, or external side effect.

Artifact playback, validation, preview visibility, candidate recommendation, advisory P2/P3 findings, and ordinary reversible changes are not approval gates.

An owner result of `baseline_change_required` is not a question gate. Invalidate the affected design dependents, generate a revised candidate whole from current sources, and pause only at `awaiting-design-approval` for approval of that revised integrated baseline. If the current source already contains an explicit scoped operator correction and acceptance, persist it as an operator override and reconcile the affected baseline scope without asking the operator to approve the same correction again.

## Prototype Candidate Contract

After the coherent pre-design SDD baseline validates, invoke the project-supported prototype producer through its adapter. It must return exactly three meaningfully distinct, whole-product, independently interactive candidates with equivalent required scope.

For each candidate require:
- candidate ID and version
- immutable visual-target reference: rendered artifact/result ID, mockup, screenshot, or frame
- frozen visual-target content hash
- frozen prototype source root and source-tree hash
- source artifact IDs/hashes
- stable live URL and route
- covered journey, screens, states, representative data, locale, and viewports
- internal visual-QA evidence
- external-default-browser open result

Open Candidate A, Candidate B, and Candidate C as three separate live pages in the operating system's external default browser. They may share one preview server, but each must have an independently addressable stable route. Embedded previews, static images, and headless captures do not satisfy this requirement.

The system may rank and recommend with rationale but must not auto-select. `Request revision` creates no approval receipt. `Approve design baseline` selects the exact candidate/version and records the only normal design approval.

Every revision creates a new candidate version, immutable target reference, and content hash. Never overwrite a candidate or approved target in place; retain prior versions and supersede them explicitly.

Treat vendor Work Mode, `terminal.local`, Sites, cloud-browser, or in-app-browser requirements as adapter transport. Persist internal `VisualQAEvidence` separately from the operator-visible browser receipt. Apply DAS Forge release-effect policy to imported findings; a vendor P2 is not automatically blocking.

Normalize `VisualQAEvidence` with adapter/environment, candidate or Baseline ID, target reference/hash, canonical preview URL, route/state/viewport/theme/content fixture, source and implementation capture IDs, interactions checked, console result, QA result, findings with severity and release effect, and timestamp. Retain raw provider reports only as attachments.

Treat image-to-code output as a Phase 2 frontend prototype. It does not prove production auth, persistence, backend/API, integrations, security boundaries, or exhaustive edge cases. Production code may reuse it only through the traced promote/diff contract in `docs/development-plan.md`. The Phase 3 runner, not this orchestrator, the planning skill, or implementation-agent prose, owns the resulting `forge/runs/{unit_id}/{run_id}/prototype-promotion.json` receipt derived from the actual Git diff.

For literal URL cloning only, require an authorized `SourceCaptureBundle` before coding. Validate the correct page and reject login/error/blocked/loading/install/promo/redirect captures; record complete small-step desktop scrolling, lazy-loaded and sticky changes, the required mobile viewport, DOM/style/layout evidence, responsive behavior, every visible control and state, and all required images, icons, fonts, videos, SVGs, stylesheets, and other assets. Treat an incomplete bundle as a typed clone blocker. Do not impose exhaustive clone capture on redesign, improvement, or inspiration routes.

## Baseline And Invalidation

The `Approved Visual Baseline` section of `docs/design-brief.md` is the single canonical baseline manifest and the visual Definition of Done for user-visible frontend implementation. After approval:
1. re-invoke `to-design-brief` to set `Status: approved`, Baseline ID, candidate/version, immutable target reference/hash, frozen prototype source root/tree hash, prototype references, coverage, receipt, visual-DoD scope, permitted variance, and supersession;
2. re-invoke `to-qa-checklist` so concrete visual checks reference the Baseline ID;
3. invoke `to-development-plan` only after both updates validate.

If a source hash changes, invalidate only transitive dependents. Keep the current approved baseline active and immutable while a revision is merely proposed. Atomically switch the active Baseline ID only when the operator approves a revised integrated whole or explicitly directs and accepts a scoped baseline correction; record the latter as an operator override without a redundant approval prompt. When a later baseline supersedes the prior one, re-invoke the QA and development-plan owners automatically and mark affected production Feature Units `execution_invalidated` in the manifest/runtime projection. This skill does not own production implementation agents; the DAS Forge Phase 3 runner dispatches them only after the regenerated plan validates. An implementation agent cannot create an override or make its own drift authoritative.

## Manifest Contract

Store at least:

```json
{
  "pipeline_version": "string",
  "state": "string",
  "artifacts": {
    "artifact_id": {
      "path": "string",
      "owner_skill": "string",
      "status": "missing|ready|running|validated|invalidated|blocked",
      "source_hashes": {},
      "content_hash": "string|null",
      "validation": {},
      "open_questions": [],
      "supersedes": "string|null"
    }
  },
  "prototype_candidates": [],
  "approved_baseline_id": "string|null",
  "active_baseline": {
    "baseline_id": "string|null",
    "visual_target_hash": "string|null",
    "prototype_tree_hash": "string|null",
    "operator_overrides": [],
    "supersedes": "string|null"
  },
  "affected_feature_units": [],
  "pause_reason": "string|null",
  "last_resume_event": "object|null",
  "next_ready_nodes": []
}
```

Do not store secrets. Use stable IDs and content hashes so resume and invalidation are deterministic.

## Workflow

1. Load or initialize the manifest from actual files; never trust stale manifest state over filesystem evidence.
2. When resuming from a product-scope answer, design-approval receipt, or risk-authorization receipt, validate and persist the response, clear `pause_reason`, recompute hashes and ready nodes, and continue automatically in the same pipeline run. Do not require a separate resume confirmation.
3. Validate `docs/product-idea.md`, then dispatch `to-prd` if required.
4. Compute ready nodes from the dependency graph and dispatch their owner skills.
5. After each result, validate the owner boundary, source traceability, required structure, open questions, and content hash.
6. Reconcile terminology and cross-artifact conflicts by re-invoking owners; never patch their artifacts directly.
7. Continue until the coherent pre-design SDD baseline validates.
8. Produce and verify the three prototype candidates, open their three external-browser pages, then pause once for whole-design selection and approval.
9. Persist the Approved Visual Baseline through its owner, update QA through its owner, and create the development plan through its owner.
10. Return the pipeline state, evidence, approved Baseline ID, invalidations, and next executable action.

## Final Report

Return:
- `Result`
- `Pipeline State`
- `Manifest`
- `Validated Artifacts`
- `Prototype Candidates And Browser Receipts`
- `Approved Baseline ID`, when approved
- `Invalidated Or Regenerated Artifacts`
- `Blocking Decision Or Authorization`, only when paused
- `Next Executable Action`
