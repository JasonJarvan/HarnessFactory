# longterm.md

## Document Meta

- Repository: `<target-repo>` (placeholder — replace with the target repository identifier on activation)
- Effective From: `<YYYY-MM-DD>` (placeholder — set when this stack is first activated in the target repo)
- Source Template: `harness-factory/assets/templates/longterm/solo.md`
- Recipe Reference: `harness-factory/assets/templates/recipes/superpowers-repomem-sendbox-dashboard.md`
- Last Updated Because: initial long-term contract; solo + long-lived platform repository with multi-worktree / subagent-dispatch work mode that requires both cross-task memory (RepoMem) and a durable inter-session channel (sendbox) plus a single-file projection of pending user actions (cc-dashboard).

## Current Long-Term Assessment

- Collaboration Scale: `solo`
- Repository Type: `platform`
- Project Horizon: `long-lived`
- Long-Term Knowledge Governance: `enabled`

## Current Active Long-Term Baseline

### 1. Primary Workflow Layer

- Default enabled: none
- Emergent Ownership: Superpowers brainstorming and writing-plans carry primary workflow responsibility for solo work.
- Default inactive: `BMAD`, `gstack`, `GSD`
- Upgrade trigger:
  - repository acquires a roadmap-heavy delivery mode
  - task portfolio grows past what execution discipline alone can carry

### 2. Spec Layer

- Default enabled: none
- Default inactive: `OpenSpec`
- Upgrade trigger:
  - a task requires stable change boundaries
  - delivery target reaches `MVP` or above
  - task risk or scope makes chat-only agreement unsafe

### 3. Execution Discipline Layer

- Default enabled: `Superpowers`
- Default inactive: none
- Upgrade trigger:
  - raise verification and review intensity when risk rises

### 4. Repository Memory Layer

- Default enabled: `RepoMem`
- Default inactive: none
- Upgrade trigger:
  - long-term memory pressure requires `RepoMem.prune / split`
  - memory governance needs harden into `ECC` hooks

### 5. Harness Enhancement Layer

- Default enabled: `sendbox-protocol`, `cc-dashboard`
- Default inactive: `ECC`, `ECC(light)`
- Upgrade trigger:
  - agent context quality, safety, or repeatability becomes a recurring problem — add `ECC(light)`
  - inter-session-comm convention is replaced by a different channel — re-evaluate dashboard fit per `methods/dashboard/embedding-playbook.md § 4`

Adoption note: sendbox + cc-dashboard are by-default `skip` for solo per their embedding-playbooks. This baseline overrides that default because the operator runs a multi-worktree / subagent-dispatch workflow. If that work mode stops, prefer leaving the layers active-but-unexercised rather than removing them (target-repo add-only).

## Pipeline

The Pipeline is the 11-step `superpowers-repomem` chain. sendbox letters and cc-dashboard rows are condition overlays, not new pipeline steps.

1. RepoMem.read — load long-term architecture and memory as task context
2. Superpowers.brainstorming — clarify vague intent
3. RepoMem.capture — open task-level temporary docs (requirement, architecture)
4. Superpowers.writing-plans — produce executable plan
5. Superpowers.using-git-worktrees + executing-plans + TDD — implement
6. RepoMem.capture (continuous) — record tacit knowledge into temporary memory
7. Superpowers.verification-before-completion — verify behavior
8. Superpowers.requesting-code-review
9. Superpowers.finishing-a-development-branch
10. RepoMem.merge (HITL) — promote stable knowledge from temporary to long-term
11. RepoMem.prune / split — periodic hygiene, not per-task

### Sendbox Triggers Across The Pipeline

Write a letter only when the Minimal Sendbox rule says you should (see `methods/sendbox/embedding-playbook.md`).

| Pipeline step | Trigger condition | Canonical letter type |
|---|---|---|
| Step 2 | Spawning a fresh recipient session (subagent, sibling worktree, inheritance) | `handoff.md` to `to<Role>/` (mode = child or inheritance) |
| Step 4–5 | Implementer awaits orchestrator greenlight | `from-<sender>-plan-ready.md` ↔ `from-<orche>-<x>-greenlight.md` |
| Step 5 | A-12 stop-and-ask hit | `from-<sender>-blocker-<topic>.md` |
| Step 7 | Vertical-slice acceptance gate hit by a subagent | `from-<sender>-<milestone>-done.md` |
| Step 8 | Orchestrator owes N decisions to one recipient | `from-<orche>-<recipient>-decisions.md` (bundled) |
| Step 9 | Branch close-out summary | `from-<sender>-archived.md` |
| Step 10 | A sendbox letter contains a lesson worth promoting to RepoMem persist | `from-<sender>-promote-to-durable.md` (route content through `RepoMem.merge`) |
| Any time | New constraint applies to every active session | `toAllActiveSessions/from-<orche>.md` (broadcast with supersession rule) |

### Dashboard Writes Across The Pipeline

One letter → N rows, one row per atomic user action. Mark-done by default option (a) — any session or the user.

| Trigger | Row count | Typical type |
|---|---|---|
| Writing `docs/sendbox/toUser/*.md` | 1..N | A / C / D |
| Writing `docs/sendbox/to<Implementer>/handoff.md` | ≥1 (at minimum "Start <Implementer> session") | B |
| Identifying a user-blocking action with no sendbox doc | 1 | C / D / F |

## Cross-Layer Conflicts

| Overlap | Conflict | Resolution |
|---|---|---|
| Plan vs memory | Superpowers.writing-plans vs RepoMem temporary requirement doc | writing-plans defines HOW; RepoMem temporary doc records WHY/context; never duplicate plan steps into memory |
| Verification vs memory | Superpowers.verification-before-completion vs RepoMem.merge | verification gates branch completion; RepoMem.merge runs after branch finishing, never as part of verification |
| Doc sedimentation | task-level temporary memory vs long-term memory | temporary memory is authoritative during the task; long-term memory only accepts content via the HITL merge step |
| Sendbox promotion vs RepoMem merge | `from-<x>-promote-to-durable.md` content vs `docs/RepoMem/persist/` | Letter content is promoted through `RepoMem.merge`, not by a parallel write path. The letter is then burned. Sendbox MUST NOT silently bypass the RepoMem HITL gate. |
| Sendbox lifecycle vs dashboard lifecycle | Burning a letter vs dashboard row status | Lifecycles are independent. Burning a letter does NOT cascade-delete any dashboard row; marking a row done does NOT trigger letter cleanup. |
| Dashboard row vs L2 tracker | A dashboard row vs a tracker (Linear / Multica / Jira) ticket | Dashboard rows are user-action granularity; tracker tickets are work-unit granularity. Do NOT mirror trackers into the dashboard. |
| Dashboard granularity vs letter content | One letter with three asks | One letter → three rows. Never collapse one letter to one row. |
| Sendbox cwd fan-out | Subagent in a side cwd writing to its own `docs/sendbox/` | Forbidden. The main agent's `docs/sendbox/` is the single source of truth. Side cwds write to it by relative or absolute path. |

## Verification Topology

- `Superpowers.verification-before-completion` is the single verification entry before `requesting-code-review`.
- RepoMem has no verification role — it does not gate completion.
- sendbox has no verification role — letters are operational. A `from-<x>-blocker-<topic>.md` is a coordination gate (agent pauses for ack), not a verification gate.
- cc-dashboard has no verification role and never gates any Superpowers pipeline step. It is read-only by the user.

## Merge Gates

- `RepoMem.merge` MUST run after `Superpowers.finishing-a-development-branch`, never before.
- `RepoMem.merge` is HITL — a human reviews promotion candidates before they enter the long-term layer.
- `from-<x>-promote-to-durable.md` content MUST flow through `RepoMem.merge`'s HITL gate before the letter is burned. No parallel promotion path.
- sendbox letter lifecycle (`burn` / `archive` / `persist`) is executed at the two sendbox cleanup checkpoints (session end, task convergence) by the authoring or receiving session — NOT by any Superpowers pipeline step.
- cc-dashboard row lifecycle (`open → done → archived → garbage-collected`) is independent of any merge gate. Mark-done is per-row, opportunistic.
- `RepoMem.prune / split` runs on a different cadence than per-task work.

## Execution Policy

| # | Step | Policy | Skip Criteria (auto-judge only) | Notes |
|---|---|---|---|---|
| 1 | RepoMem.read | auto | — | Read-only context load. Idempotent. |
| 2 | Superpowers.brainstorming | auto-judge | Intent is already `clear` per task contract, or task is a trivial fix / pure refactor. | When a subagent is being spawned, write sendbox `handoff.md` before brainstorming hands off context. |
| 3 | RepoMem.capture (open temp docs) | auto | — | Mechanical folder creation. |
| 4 | Superpowers.writing-plans | auto-judge | Single-step task with no branching, or `<3h test` delivery target. | If the plan is produced by a subagent, write `from-<sender>-plan-ready.md` for orchestrator greenlight. |
| 5 | using-git-worktrees + executing-plans + TDD | auto-judge | No isolation needed; small change with no parallel work. TDD scope follows plan. | Worktree decision is judged; TDD discipline is not. A-12 blocker letter MAY fire here. |
| 6 | RepoMem.capture (continuous) | auto | — | Passive tacit-knowledge recording. |
| 7 | Superpowers.verification-before-completion | auto | — | Behavior verification is non-negotiable. Subagent `milestone-done` letter MAY fire here. |
| 8 | Superpowers.requesting-code-review | ask-first | — | External visibility: opens a review request. Confirm before triggering. Bundled `decisions.md` letters MAY be written here. |
| 9 | Superpowers.finishing-a-development-branch | ask-first | — | Multi-step git state change. Confirm scope. `from-<sender>-archived.md` MAY be written here. |
| 10 | RepoMem.merge | HITL | — | Contract-mandated human review. Never downgradable. Any `from-<x>-promote-to-durable.md` content lands here. |
| 11 | RepoMem.prune / split | auto | — | Periodic hygiene, not per-task. Runs on its own cadence. |

Sendbox letter writes and cc-dashboard row writes are side-effects of the above steps, not standalone pipeline steps.

## Suitability Envelope

### Fits

- one active contributor who routinely dispatches subagents or runs multi-worktree parallel work
- long-lived platform / library / methodology repositories where architecture and decisions accumulate AND multi-session coordination is recurring
- changes that do not need explicit spec boundaries
- risk low to medium

### Does Not Fit

- solo work that is strictly single-session, linear, no subagents — drop to `superpowers-repomem`
- short-lived or disposable repositories — drop to `superpowers`
- changes that need durable spec boundaries — extend to a future `openspec-superpowers-repomem-sendbox-dashboard`
- multi-team large-scale coordination — needs a heavier primary workflow layer

## Temporary Contractor Boundary Rules

### Temporary Contractor May Adjust

- add `OpenSpec` for a single task (and declare the addition in the task contract)
- raise or lower `Superpowers` intensity
- enable lightweight `ECC` for a task
- skip `RepoMem.capture` for trivial `<3h test` tasks (still must read long-term memory)
- choose not to exercise sendbox / cc-dashboard for a single-session linear task — declare the suppression in the task contract; do NOT remove the layers from the long-term baseline

### Temporary Contractor May Not Override

- the existence of long-term repository memory once enabled
- long-term governance and safety constraints
- the sendbox single-source-of-truth principle (one `docs/sendbox/` per project, held by the main agent — see Cross-Method Invariants)
- cc-dashboard's hard dependency on sendbox (cannot exercise dashboard without sendbox)
- pipeline ordering, merge gates, and verification topology — recipe invariants; exceptions require a declared `Recipe Invariant Exceptions` section with reason and compensating action
- this document's collaboration-scale assumption without full rewrite

## Full Rewrite Conditions

- repository moves from solo to team collaboration
- repository horizon flips to short-lived
- default primary workflow needs to become permanently heavier
- the operator stops doing multi-worktree / subagent-dispatch work permanently AND chooses to retire the sendbox + dashboard layers (note: per add-only, prefer leaving them active-but-unexercised)

(Note: switching from `superpowers-repomem-sendbox-dashboard` to a superset recipe such as a future `openspec-superpowers-repomem-sendbox-dashboard` is an extension under add-only — update `Recipe Reference` in place; not a full rewrite.)

## Related Documents

- `docs/HarnessStack/temporary-<task>.md` (when a task is in progress)
- `docs/RepoMem/persist/version-plan.md`
- `docs/HarnessStack/hooks/cc-dashboard.md` (hook config with repo-local Language Policy — created on activation)
- Related RepoMem architecture and memory docs

## Hooks

| Hook | Status | Purpose |
|---|---|---|
| [`hooks/cc-dashboard.md`](hooks/cc-dashboard.md) | active | Maintain `docs/Dashboard/index.md` as SSOT for pending user actions; trigger on any session write to `docs/sendbox/` or identification of a new user-blocking action |

## Cross-Method Invariants

These rules bind HarnessStack to its companion methods. They are not part of any single layer and therefore live here at the long-term contract level.

- **Single task identifier.** The RepoMem `<slug>` and the HarnessStack `<task>` MUST be the same string: `<task>` = `<slug>`. Diverging on naming defeats per-task cross-referencing.
- **No content duplication across per-task document sets.** RepoMem temp docs (`docs/RepoMem/temp/<slug>/`) and the HarnessStack per-task contract (`docs/HarnessStack/temporary-<task>.md`) each answer a distinct question and MUST NOT restate each other's content. The reviewer at `RepoMem.merge` rejects (deletes, does not merge) any temp content that duplicates the HarnessStack temporary record.
- **Multi-session work uses sendbox-protocol.** When a task involves multiple
  sessions, dispatched subagents, or cross-worktree coordination, the
  `sendbox-protocol` skill (see `~/.claude/skills/sendbox-protocol/SKILL.md`)
  is the canonical asynchronous channel. The main agent's `docs/sendbox/` is
  the single source of truth, and subagents in side cwds write to it by
  relative or absolute path — never fan out under their own cwd. See
  `methods/sendbox/embedding-playbook.md` for the embedding playbook.
- **Pending user actions are projected into a single dashboard.** When sendbox-protocol is active, the `cc-dashboard` skill (see `~/.claude/skills/cc-dashboard/SKILL.md`) maintains `docs/Dashboard/index.md` as the single source of truth for pending user actions. Any session writing a `toUser/` letter or a `to<Implementer>/handoff.md` MUST append one row per atomic user action. Mark-done lifecycle is independent from letter lifecycle. See `methods/dashboard/embedding-playbook.md` for the embedding playbook.
- **Sendbox-to-RepoMem promotion goes through `RepoMem.merge`.** A `from-<x>-promote-to-durable.md` letter is a *candidate* for long-term knowledge; the actual write into `docs/RepoMem/persist/` happens through the `RepoMem.merge` HITL gate, never via a parallel path. The letter is burned after merge.
- Divergence from any rule above requires a `Recipe Invariant Exception` in the task contract with reason and compensating action.
