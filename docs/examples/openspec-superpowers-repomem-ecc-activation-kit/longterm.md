# longterm.md

## Document Meta

- Repository: <TODO: target repo name>
- Effective From: <TODO: YYYY-MM-DD>
- Source Template: harness-stack/assets/templates/longterm/small-team.md
- Recipe Reference: harness-stack/assets/templates/recipes/openspec-superpowers-repomem-ecc.md
- OpenSpec Root: <TODO: ./openspec/ (OpenSpec default) | docs/openspec/ (co-located with other method-layer artifacts)>
- Last Updated Because: Initial baseline activating openspec-superpowers-repomem-ecc for small-team scale.

> Note on Recipe Reference: this field is single-value. If team tooling is
> not ready for full ECC(medium) on day one, the recommended path is to
> activate the leaner parent recipe `openspec-superpowers-repomem` first and
> switch this field to the ECC superset later — that switch is an add-only
> extension event, recorded in `Last Updated Because`. The leaner option
> itself does not live in this field; see kit README § Step 5 for the
> downgrade path during initial activation.

## Current Long-Term Assessment

- Collaboration Scale: small-team
- Repository Type: <TODO: product | research | platform | other>
- Project Horizon: long-lived
- Long-Term Knowledge Governance: enabled

## Current Active Long-Term Baseline

### 1. Primary Workflow Layer

- Active: none (emergent)
- Emergent Ownership: OpenSpec change cycle (proposal → specs → tasks →
  archive) plus Superpowers brainstorming and writing-plans jointly carry
  primary workflow responsibility.
- Default inactive: BMAD, gstack, GSD
- Upgrade trigger:
  - cross-task coordination cost becomes persistently high
  - active contributors exceed small-team threshold
  - multi-quarter roadmap planning required

### 2. Spec Layer

- Active: OpenSpec
- Default inactive: none
- Upgrade trigger: parallel changes start interacting and require strict enforcement

### 3. Execution Discipline Layer

- Active: Superpowers
- Default inactive: none
- Upgrade trigger: raise verification and review intensity for risky work

### 4. Repository Memory Layer

- Active: RepoMem
- Default inactive: none
- Upgrade trigger: split architecture and memory more aggressively as domains grow

### 5. Harness Enhancement Layer

- Active: ECC(medium)
- Default inactive: none
- Upgrade trigger:
  - shared context, safety, or repeatability becomes a recurring problem
  - promote to ECC(strong) when stricter governance, audit, or eval gating is needed

> Note: The five cross-layer sections below are rendered against the default
> recipe `openspec-superpowers-repomem-ecc`. If you switch `Recipe Reference`
> to a different recipe, re-render these sections from that recipe before
> continuing.

## Pipeline

1. ECC.research-first — pull current library / API / pattern docs relevant to
   the task (Context7 or equivalent MCP)
2. RepoMem.read — load long-term architecture and memory as task context
3. Superpowers.brainstorming — clarify vague intent (consumes research-first
   output and RepoMem context)
4. OpenSpec.explore / propose — convert intent into a formal change with specs
5. RepoMem.capture — open task-level temporary docs (requirement, architecture)
6. Superpowers.writing-plans — consume OpenSpec specs and tasks to produce
   executable plan
7. Superpowers.using-git-worktrees + executing-plans + TDD — implement
8. RepoMem.capture (continuous) — record tacit knowledge into temporary memory
9. ECC.session-state.persist (continuous) — persist agent session state across
   restarts; harness-level, distinct from RepoMem
10. ECC.pre-commit-eval — fast mechanical gate (format, lint, smoke evals)
11. ECC.security-scan — run when dependencies change, and again pre-archive
12. Superpowers.verification-before-completion + OpenSpec.verify —
    dual-perspective behavior verification
13. Superpowers.requesting-code-review
14. Superpowers.finishing-a-development-branch
15. OpenSpec.archive — freeze change record (gated by ECC.security-scan when
    dependencies changed)
16. RepoMem.merge (HITL) — promote stable knowledge from temporary to long-term
17. RepoMem.prune / split — periodic hygiene, not per-task

## Cross-Layer Conflicts

| Overlap | Conflict | Resolution |
|---|---|---|
| Early-phase intent convergence | Superpowers.brainstorming vs OpenSpec.explore | brainstorming first when intent is vague; switch to OpenSpec once intent is formalizable as a change intent |
| Plan concept | Superpowers.writing-plans vs OpenSpec.tasks | OpenSpec.tasks defines WHAT contract; writing-plans defines HOW execution; the latter consumes the former |
| Verification | OpenSpec.verify vs Superpowers.verification-before-completion | run both — different lenses |
| Doc sedimentation | OpenSpec change docs vs RepoMem memory | OpenSpec is the authoritative source per change; RepoMem extracts durable lessons at archive time and never duplicates the change record. See § Task Identifier and Document Boundary for the binding rule. |
| Context bootstrap | ECC.research-first vs Superpowers.brainstorming | research-first is read-only doc lookup; brainstorming consumes its output to shape intent. Run research-first first. |
| State persistence | ECC.session-state vs RepoMem.capture | ECC session-state is harness-level agent state (across restarts); RepoMem.capture is repo-level knowledge artifacts. Do not duplicate; agent runtime state never enters RepoMem. |
| Pre-commit checks | ECC.pre-commit-eval vs Superpowers.verification-before-completion | pre-commit-eval is a fast mechanical gate (format, lint, smoke); verification-before-completion is semantic (did we satisfy the change). Both run; the latter cannot be skipped just because the former passes. |

## Verification Topology

- ECC.pre-commit-eval — "do basic mechanical and smoke checks pass?" (fast)
- ECC.security-scan — "did any dependency / supply-chain risk regress?" (run
  on dependency change and pre-archive)
- OpenSpec.verify — "did we deliver what the spec promised?"
- Superpowers.verification-before-completion — "is the implemented behavior
  actually correct?"
- All four lenses are required for changes that touch dependencies; the first
  three are required for code-only changes.
- A change cannot enter `finishing-a-development-branch` unless OpenSpec.verify
  and Superpowers.verification-before-completion pass.
- A change cannot enter `OpenSpec.archive` unless ECC.security-scan passes when
  dependencies changed in this change.

## Merge Gates

- RepoMem.merge MUST run after OpenSpec.archive, never before.
- ECC.security-scan MUST pass before OpenSpec.archive whenever the change
  touches dependencies.
- RepoMem.merge is HITL — a human reviews promotion candidates before they
  enter the long-term layer.
- RepoMem.prune / split runs on a different cadence than per-task work.
- ECC.session-state persistence is continuous and is never gated by a merge.

## Execution Policy

Per-step runtime mode. Copied verbatim from
`harness-stack/assets/templates/recipes/openspec-superpowers-repomem-ecc.md`.

| # | Step | Policy | Skip Criteria (auto-judge only) | Notes |
|---|---|---|---|---|
| 1 | ECC.research-first | auto | — | Read-only doc fetch. Idempotent. |
| 2 | RepoMem.read | auto | — | Read-only context load. |
| 3 | Superpowers.brainstorming | auto-judge | Intent is already `clear` per task contract, or task is a trivial fix / pure refactor. | When skipped, OpenSpec.explore consumes the user prompt directly. |
| 4 | OpenSpec.explore / propose | auto-judge | Trivial fix / pure refactor / `<3h test` / declared spike with no spec impact. | Skipping #4 implies skipping #15 (archive) — log both together. |
| 5 | RepoMem.capture (open temp docs) | auto | — | Mechanical folder creation. |
| 6 | Superpowers.writing-plans | auto-judge | OpenSpec.tasks already lists atomic steps that map 1:1 to execution. | When skipped, agent executes OpenSpec.tasks directly. |
| 7 | using-git-worktrees + executing-plans + TDD | auto-judge | No isolation needed; small change with no parallel work. TDD scope follows plan. | Worktree decision is judged; TDD discipline is not. |
| 8 | RepoMem.capture (continuous) | auto | — | Passive tacit-knowledge recording. |
| 9 | ECC.session-state.persist (continuous) | auto | — | Harness-layer state persistence. Never gated. |
| 10 | ECC.pre-commit-eval | auto | — | Mechanical gate (format, lint, smoke). Tool-driven. |
| 11 | ECC.security-scan | ask-first | — | Findings require accept-vs-fix value judgment — present results, await direction. Skip when the change touches no dependencies (declare via `Recipe Invariant Exception`). |
| 12 | verification-before-completion + OpenSpec.verify | auto | — | Both lenses required. Read-only behavior + spec verification. |
| 13 | Superpowers.requesting-code-review | ask-first | — | External visibility: opens a review request to humans. Confirm before triggering. |
| 14 | Superpowers.finishing-a-development-branch | ask-first | — | Multi-step git state change. Confirm scope before executing. |
| 15 | OpenSpec.archive | ask-first | — | Half-irreversible: freezes change record. Gated by #11 when deps changed. Confirm completeness first. |
| 16 | RepoMem.merge | HITL | — | Contract-mandated human review. Never downgradable. |
| 17 | RepoMem.prune / split | auto | — | Periodic hygiene, not per-task. Runs on its own cadence. |

Semantics:

- `auto` — agent runs directly, no announcement, no wait.
- `auto-judge` — agent decides at runtime whether to run or skip; does NOT
  interrupt the user. Skip decisions are logged one line in
  `temporary-<task>.md § Auto-Skip Log`.
- `ask-first` — agent announces (1–2 lines) and waits for user confirmation.
- `HITL` — contract-mandated human review. Never downgradable.

Skip mechanism selection (also rendered in `temporary-<task>.md § Mechanism
Selection`):

- Skipping an `auto-judge` step because its Skip Criteria triggered →
  `Auto-Skip Log` (lightweight)
- Skipping an `auto` / `ask-first` / `HITL` step, OR skipping an `auto-judge`
  step whose Skip Criteria did NOT trigger → `Recipe Invariant Exceptions`
  (heavyweight; reason + compensating action required)

## Cross-Method Invariants

This section is a recipe-level invariant. It removes the only operational
ambiguity between OpenSpec and RepoMem at task scope — without it, the
"Doc sedimentation" resolution above relies on convention rather than
rule.

### Single Task Identifier

For any task that produces an OpenSpec change AND any RepoMem temp docs,
the following three identifiers MUST be the same string:

- the OpenSpec `change-id` (folder name under `openspec/changes/`)
- the RepoMem `<slug>` (folder name under `docs/RepoMem/temp/`)
- the HarnessStack `<task>` (suffix of `docs/HarnessStack/temporary-<task>.md`)

That is: `<task>` = `change-id` = `<slug>`. This is the only mechanism
that keeps the three per-task document sets cross-referenceable without
manual mapping. Diverging on naming forces every reader and every tool to
reconcile by hand, which defeats the kit's coordination contract.

### Per-Task Document Boundary

Three document sets coexist per task. Each answers a distinct question
and MUST NOT duplicate the others:

| Document set | Question it answers | Authoritative for |
|---|---|---|
| `openspec/changes/<id>/{proposal,design,tasks,specs}` | What is the change contract? | requirement statements, behavior deltas, technical approach, implementation checklist |
| `docs/RepoMem/temp/<slug>/{requirements,architecture,memory}` | What did we learn that outlives this change? | tacit knowledge, decisions and trade-offs not captured in change docs, cross-task implications |
| `docs/HarnessStack/temporary-<task>.md` | How is this task being executed? | task-scope contractor config, recipe invariant exceptions, delivery target, risk level |

### Hard Rules

- RepoMem.capture MUST NOT restate content that already lives in the
  matching OpenSpec change docs. If overlap occurs, the OpenSpec doc is
  canonical and the RepoMem entry is redundant.
- A `temp/<slug>/requirements.md` entry is permitted only when it
  captures context the change `proposal.md` cannot — e.g., upstream
  constraints, rejected alternatives, dependencies on other repos.
- A `temp/<slug>/architecture.md` entry is permitted only when it
  captures durable architectural insight worth promoting later — e.g.,
  constraints discovered during implementation that change how this
  domain should evolve.
- `temp/<slug>/memory.md` is the default landing for tacit knowledge and
  has no overlap with OpenSpec by definition.
- A reviewer MAY block `RepoMem.merge` when temp content duplicates the
  archived OpenSpec change record. Such content is deleted, not merged.

### Enforcement

- `OpenSpec.verify` and `Superpowers.verification-before-completion` do
  not enforce this boundary; the temporary contractor and the human
  reviewer at `RepoMem.merge` are the enforcement points.
- A different `change-id` and `<slug>` (or a missing
  `temporary-<task>.md`) is a declared `Recipe Invariant Exception` in
  `temporary-<task>.md` with reason and compensating action — silent
  divergence is forbidden.

## Suitability Envelope

### Fits

- 2 to 5 contributors (small-team scale)
- long-lived product or platform repositories
- changes can be sliced into discrete change units
- risk medium to high
- shared context, lightweight pre-commit eval, or dependency security scan are
  valued enough to justify ECC overhead

### Does Not Fit

- pure spike or probe experiments — OpenSpec friction is too high
- short-lived repos — RepoMem overhead is unjustified
- solo, low-stakes — switch to a lighter recipe (`openspec-superpowers-repomem`
  or `superpowers`)
- multi-team large-scale coordination — extend to a recipe with a primary
  workflow (BMAD or GSD prefix)

## Temporary Contractor Boundary Rules

### Temporary Contractor May Adjust

- choose lighter or heavier task-level flow based on clarity and delivery target
- reduce OpenSpec intensity for tiny low-risk tasks
- raise or lower Superpowers and ECC intensity for risky work

### Temporary Contractor May Not Override

- the existence of OpenSpec, RepoMem, Superpowers, or ECC as the team baseline
- long-term collaboration and governance rules
- this document's collaboration-scale assumption without full rewrite
- Pipeline ordering, Merge Gate sequencing, or Verification Topology — these
  are recipe-level invariants. The temporary contractor MAY skip one only by
  declaring the exception in its `Recipe Invariant Exceptions` section, with
  reason and compensating action. Default is deny — silent skips are forbidden.

## Full Rewrite Conditions

- team scale changes materially (small-team → solo or large-team)
- repository switches to heavier coordination requiring a primary workflow
- default baseline changes the active layers materially

(Note: switching `Recipe Reference` to a superset recipe — e.g., upgrading
from ECC(medium) to ECC(strong), or extending to a primary-workflow recipe —
is an extension event, not a rewrite; update in place. Whether to drop a
layer is the project's call. HarnessStack's recommended pattern is to extend
rather than replace, but this document does not bind the project.)

## Related Documents

- docs/HarnessStack/temporary-<task>.md
- docs/RepoMem/persist/version-plan.md
- docs/RepoMem/persist/architecture/
- docs/RepoMem/persist/memory/
- harness-stack/assets/templates/recipes/openspec-superpowers-repomem-ecc.md
