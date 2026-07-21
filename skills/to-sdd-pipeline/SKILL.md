---
name: to-sdd-pipeline
description: Orchestrate a design-first SDD pipeline from a validated foreground Product Idea Intake handoff or existing docs/product-idea.md through PRD, the project-context/canonical-terms bundle, the coherent pre-design SDD baseline, exactly three runnable prototype candidates, one whole-design approval, post-approval reconciliation, and docs/development-plan.md. Use when the user wants the full SDD set generated or reconciled autonomously rather than invoking one artifact skill at a time.
---
# to-sdd-pipeline

## Mission

Run the SDD workflow as one autonomous dependency graph while preserving exclusive artifact ownership. The process exists to reduce an engineer's coordination work. Do not add file-by-file, screen-by-screen, or step-by-step approval gates.

Treat Product Idea Intake as the visible Phase 0 immediately upstream of this graph. Never silently invent or generate missing product intent. When `docs/product-idea.md` is absent or materially incomplete, dispatch or resume `to-product-idea` through the DAS Forge foreground intake adapter and return `awaiting-product-idea-intake`; do not continue into PRD generation.

## Input

Require:
- `docs/product-idea.md`
- the artifact-owner skills listed below
- a project-supported prototype producer or Product Design adapter before the prototype node runs

In DAS Forge, also require a current `ProductIdeaHandoffReceipt` whose recorded content hash matches `docs/product-idea.md`. A manually authored or imported idea becomes eligible through the same visible `Create product idea and start SDD` command after validation; do not force a new interview when its intent is already coherent. In a direct non-DAS invocation, a validated existing file may serve as the handoff source and must be recorded as `source_mode: existing-file` in the manifest.

Read existing SDD artifacts and `forge/sdd-manifest.json` when present. Inspect the codebase for source-backed architecture, design-system, runtime, and verification facts instead of asking for discoverable information.

## Output And Ownership

This orchestrator directly creates or updates exactly one file:
- `forge/sdd-manifest.json`

It must never directly create or edit a domain artifact. Invoke or re-invoke the owning skill:

| Artifact | Owner |
|---|---|
| `docs/product-idea.md` | `to-product-idea` (foreground Phase 0; only invoked when missing, incomplete, imported for intake, or changed by an explicit upstream decision) |
| `docs/prd.md` | `to-prd` |
| `docs/project-context.md` | `to-project-context` |
| `docs/canonical-terms.md` | `to-project-context` |
| `docs/guardrails.md` | `to-guardrails` |
| `docs/user-journey.md` | `to-user-journey` |
| `docs/screen-map.md` | `to-screen-map` |
| `docs/wireframes.md` | `to-wireframes` |
| `docs/design-brief.md` | `to-design-brief` |
| `docs/architecture.md` | `to-architecture` |
| `docs/dod-evals.md` | `to-dod-evals` |
| `docs/qa-checklist.md` | `to-qa-checklist` |
| `docs/development-plan.md` | `to-development-plan` |

An owner invocation may change only its declared artifact path or declared cohesive output set. `to-project-context` is one coupled two-output owner invocation: both files are required, validated and hashed separately, and recorded with the same owner-invocation ID. A missing, stale, or invalid member makes `project-context-bundle` incomplete and re-invokes that owner for the whole bundle. Every artifact still has exactly one owner. The orchestrator validates owner output, records its hash and provenance, then dispatches every newly ready node without asking the user to continue.

The prototype producer is a runtime adapter, not an SDD artifact owner. During Phase 2 it may write candidate-specific code/assets only under `forge/design/candidates/{candidate_id}/{version}/`, optional shared preview infrastructure only under the versioned `forge/design/candidate-sets/{candidate_set_id}/{set_version}/shared/` workspace, and normalized evidence under `forge/design/evidence/`. Shared runtime reuse resolves to that candidate-set version and cannot hide mutable source elsewhere. It must not write production application source directories, domain SDD artifacts, or the orchestration manifest. Every write records adapter, candidate/version or candidate-set version, target hash, and changed paths. Phase 3 implementation agents own production-code writes under the bounds of the approved development plan.

## Dependency Graph

Use this acyclic graph:

```text
product-idea-intake
-> product-idea
-> prd
-> project-context-bundle
   |- project-context
   `- canonical-terms
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

In pipeline mode, `to-project-context` reads only the product idea, PRD, explicit user decisions, README/CODEX, and independent project evidence; it never reads downstream SDD artifacts back into the context bundle. `docs/guardrails.md` depends only on the PRD, the validated context bundle, and explicitly authoritative upstream intent; it never reads downstream artifacts back into itself. `docs/wireframes.md` never depends on `docs/design-brief.md`. `docs/development-plan.md` never belongs to the pre-design baseline because it requires the Approved Visual Baseline.

Run independent ready nodes in parallel when their owner skills and workspace safety allow it. Serialize nodes that share a source file being updated.

## Product Idea Intake Handoff Contract

Product Idea Intake is a Product Creation Run, not a Feature Unit. It must appear in Mission Control as a dedicated foreground workspace with one current question, its recommended answer and rationale, custom-answer controls, live draft preview, and decision coverage. A question may never exist only in terminal output or a hidden agent log.

Use `to-product-idea` as the sole owner of `docs/product-idea.md`. The DAS Forge `ProductIdeaIntake` runtime adapter owns durable session/draft state and the handoff receipt under `forge/intake/`. It must:

- emit and persist one typed `ProductIntentQuestion` at a time;
- project an unanswered material question as `Input needed`, not `Blocked` or an approval;
- route the operator's external default browser to the exact pending intake request when the intake surface is not active;
- restore the current question, answers, draft version, assumptions, and decision branch after restart;
- resume automatically after each answer without a separate continuation command;
- never convert a timeout, silence, recommendation, or non-response into consent for material product intent;
- materialize and hash `docs/product-idea.md` only after the operator invokes `Create product idea and start SDD`;
- write `forge/intake/product-idea-handoff.json` with at least intake/session ID, source mode, artifact path, content hash, answered decision IDs, assumptions, unresolved non-blocking questions, submission event, and timestamp.

`Create product idea and start SDD` is the initial execution command, not an approval receipt. Draft playback, answering questions, editing prior answers, resuming intake, and submitting intent do not add approval gates. The only normal product-creation approval remains approval of the complete integrated design baseline.

If a downstream owner discovers missing material product intent, suspend only the affected dependency branch, route one scoped question through the same intake UI, persist the answer, re-invoke `to-product-idea`, and invalidate only transitive dependents of the changed idea hash. Unrelated safe work may continue when ownership and dependencies remain unambiguous.

## Project Context Bundle Contract

Immediately after `docs/prd.md` validates, invoke `to-project-context` once to produce:

- `docs/project-context.md`
- `docs/canonical-terms.md`

Both outputs must validate from the same current PRD/product-intent source set and owner-invocation ID before `guardrails` or any later node becomes ready. Their assumptions and non-blocking open questions remain visible but do not create approval gates.

Pass both validated files to every downstream artifact owner as candidate upstream sources. Owners must use only relevant confirmed context and exact canonical vocabulary:

- `project-context.md` may supply users, platforms, localization, boundaries, constraints, dependencies, operational risks, and other confirmed context, but cannot add or override product behavior, architecture, guardrails, design, DoD, or QA truth;
- `canonical-terms.md` governs downstream naming and aliases only; it cannot redefine PRD behavior or silently rename established technical identifiers;
- assumptions remain assumptions, and descriptive or irrelevant content must not be copied merely to prove the files were read.

For each downstream artifact, record only the exact context sections or canonical-term entries it consumed in that artifact's manifest provenance. Hash those consumed fragments independently so an unrelated prose edit does not invalidate the whole pipeline. A change to a consumed context fact or term invalidates only its transitive dependents. A PRD or authoritative product-intent change invalidates both bundle members together. If the bundle exposes an upstream contradiction, re-invoke the upstream owner first and then regenerate the bundle; never patch the PRD from `to-project-context` or create a dependency cycle.

## Autonomy And Stop Rules

Resolve non-material uncertainty from source files, codebase evidence, or the smallest reversible source-grounded default. Record the decision and continue.

Pause only for:
1. Product Idea Intake or a later genuinely non-inferable decision that materially changes product scope, surfaced through a foreground `Input needed` request;
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

Store `project-context` and `canonical-terms` as two separate entries in `artifacts`. Both entries use `owner_skill: to-project-context`, the same non-null `owner_invocation_id`, and the same two-member `declared_output_set`; their content hashes and validation results remain independent.

```json
{
  "pipeline_version": "string",
  "state": "string",
  "product_idea_intake": {
    "status": "not_started|awaiting_answer|ready_to_submit|handed_off|superseded",
    "intake_id": "string|null",
    "source_mode": "seed|interview|imported|existing-file|null",
    "handoff_receipt_path": "string|null",
    "product_idea_hash": "string|null",
    "current_request_id": "string|null"
  },
  "artifacts": {
    "artifact_id": {
      "path": "string",
      "owner_skill": "string",
      "owner_invocation_id": "string|null",
      "declared_output_set": [],
      "status": "missing|input_needed|ready|running|validated|invalidated|blocked",
      "mission_control_status": "Pending|Input needed|Running|Ready|Needs attention|Approved design|Blocked|Done",
      "source_version": "string|null",
      "source_hashes": {},
      "consumed_source_fragments": {},
      "dependencies": [],
      "dependency_status": {},
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
  "input_requests": [],
  "pause_reason": "string|null",
  "last_resume_event": "object|null",
  "next_ready_nodes": []
}
```

Artifact `status` is orchestration state, while `mission_control_status` is its operator-facing projection. Map an unanswered material question to internal `input_needed` and operator-facing `Input needed`; it is neither a failure nor an approval. Map `validated` to `Done`, `invalidated` to `Needs attention` until it becomes ready again, and `blocked` to `Blocked`; `ready` means machine-ready for dispatch and is never an approval. `Approved design` is reserved for the active whole-design baseline state, not ordinary artifact completion. Keep `source_version`, `source_hashes`, `dependencies`, and `dependency_status` explicit for every artifact so readiness and invalidation do not have to be inferred from prose or filesystem order.

Do not store secrets. Use stable IDs and content hashes so resume and invalidation are deterministic.

## Workflow

1. Load or initialize the manifest from actual files; never trust stale manifest state over filesystem evidence.
2. If `docs/product-idea.md` or its DAS Forge handoff is missing, stale, or materially incomplete, set `awaiting-product-idea-intake`, dispatch or resume `to-product-idea` through the foreground adapter, persist the typed request, and return control without launching downstream owners.
3. When `Create product idea and start SDD` supplies a valid matching handoff receipt, clear the intake pause and continue automatically. Do not request another confirmation.
4. When resuming from a later product-scope answer, design-approval receipt, or risk-authorization receipt, validate and persist the response, clear `pause_reason`, recompute hashes and ready nodes, and continue automatically in the same pipeline run. Do not require a separate resume confirmation.
5. Validate `docs/product-idea.md` and its current handoff hash, dispatch `to-prd` if required, then invoke `to-project-context` once for the two-file bundle. Validate both members separately, verify their shared owner-invocation ID and current source hashes, and do not make `guardrails` ready until both pass.
6. Compute ready nodes from the dependency graph and dispatch their owner skills with the validated context bundle available as relevance-scoped upstream sources.
7. After each result, validate the owner boundary, source traceability, required structure, open questions, and content hash. Convert a material non-inferable product-intent question into a typed `Input needed` request instead of leaving it in background logs.
8. Reconcile terminology against `docs/canonical-terms.md` and cross-artifact conflicts by re-invoking owners; never patch their artifacts directly. Record only consumed context/term fragments so unrelated bundle edits do not trigger broad invalidation.
9. Continue until the coherent pre-design SDD baseline validates.
10. Produce and verify the three prototype candidates, open their three external-browser pages, then pause once for whole-design selection and approval.
11. Persist the Approved Visual Baseline through its owner, update QA through its owner, and create the development plan through its owner.
12. Return the pipeline state, evidence, approved Baseline ID, invalidations, and next executable action.

## Final Report

Return:
- `Result`
- `Pipeline State`
- `Manifest`
- `Product Idea Intake And Handoff`
- `Validated Artifacts`
- `Prototype Candidates And Browser Receipts`
- `Approved Baseline ID`, when approved
- `Invalidated Or Regenerated Artifacts`
- `Blocking Decision Or Authorization`, only when paused
- `Input Needed`, only when awaiting an operator answer
- `Next Executable Action`
