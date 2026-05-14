# longterm.md (orient — modification-direction version)

> Sibling of `openspec-superpowers-repomem-longterm.md`.
> Same scenario inputs and Mode B output, but with every problem found in
> evaluation patched. Each patch is labeled with its fix code.

## Modifications Applied (delta vs raw)

| Fix | Problem | Where applied |
|---|---|---|
| A1 | Pipeline semantics lost | New section `Pipeline` |
| A2 | Cross-layer conflicts not represented | New section `Cross-Layer Conflicts` |
| A3 | Verification topology compressed | New section `Verification Topology` |
| A4 | Merge gate timing missing | New section `Merge Gates` |
| A5 | Suitability envelope absent | New section `Suitability Envelope` |
| B1 | Layer-first entry missing | Added `Recipe Reference` in `Document Meta` |
| B2 | Same combo varies by scale | `Recipe Reference` makes the binding explicit |
| C1 | Primary `none` is ambiguous | New field `Emergent Ownership` under Primary |
| Boundary | Recipe-level invariants must not be patched by temporary | Added one item under `Temporary Contractor May Not Override` |
| Rewrite | Recipe replacement is also a rewrite event | Added one item under `Full Rewrite Conditions` |

---

## Skill Inputs (declared)

- Layer choices (pre-fixed by user): `OpenSpec + Superpowers + RepoMem`
- Implied scenario: small-team / product / long-lived / governance=enabled
- Recipe matched: `openspec-superpowers-repomem`
- Output mode: Mode B; no current task.

## Document Meta

- Repository: <target-repo>
- Effective From: 2026-05-07
- Source Template: harness-stack/assets/templates/longterm-template.md
- Recipe Reference: harness-stack/assets/templates/recipes/openspec-superpowers-repomem.md   <!-- Fix B1, B2 -->
- Last Updated Because: Initial baseline using OpenSpec + Superpowers + RepoMem combination.

## Current Long-Term Assessment

- Collaboration Scale: small-team
- Repository Type: product
- Project Horizon: long-lived
- Long-Term Knowledge Governance: enabled

## Current Active Long-Term Baseline

### 1. Primary Workflow Layer

- Default enabled: none by default
- Emergent Ownership: OpenSpec change cycle (proposal → specs → tasks → archive) plus Superpowers brainstorming/writing-plans jointly carry primary workflow responsibility.   <!-- Fix C1 -->
- Default disabled: BMAD, gstack, GSD
- Upgrade trigger:
  - cross-task coordination cost becomes persistently high
  - active contributors exceed small-team threshold
  - multi-quarter roadmap planning required

### 2. Spec Layer

- Default enabled: OpenSpec
- Default disabled: none
- Upgrade trigger: parallel changes start interacting and require strict enforcement

### 3. Execution Discipline Layer

- Default enabled: Superpowers
- Default disabled: none
- Upgrade trigger: raise verification and review intensity for risky work

### 4. Repository Memory Layer

- Default enabled: RepoMem
- Default disabled: none
- Upgrade trigger: split architecture and memory more aggressively as domains grow

### 5. Harness Enhancement Layer

- Default enabled: none
- Default disabled: ECC
- Upgrade trigger: when shared context, safety, or repeatability becomes a recurring problem

## Pipeline (Fix A1)

1. RepoMem.read — load long-term architecture and memory as task context
2. Superpowers.brainstorming — clarify vague intent
3. OpenSpec.explore / propose — convert intent into a formal change with specs
4. RepoMem.capture — open task-level temporary docs (临时需求 / 临时架构)
5. Superpowers.writing-plans — consume OpenSpec specs and tasks to produce executable plan
6. Superpowers.using-git-worktrees + executing-plans + TDD — implement
7. RepoMem.capture (continuous) — record tacit knowledge into temporary memory
8. Superpowers.verification-before-completion + OpenSpec.verify — dual-perspective verification
9. Superpowers.requesting-code-review
10. Superpowers.finishing-a-development-branch
11. OpenSpec.archive — freeze change record
12. RepoMem.merge (HITL) — promote stable knowledge from temporary to long-term layer
13. RepoMem.prune / split — periodic hygiene, not per-task

## Cross-Layer Conflicts (Fix A2)

| Overlap | Conflict | Resolution |
|---|---|---|
| Early-phase intent convergence | Superpowers.brainstorming vs OpenSpec.explore | brainstorming first when intent is vague; switch to OpenSpec once intent is formalizable as change intent |
| Plan concept | Superpowers.writing-plans vs OpenSpec.tasks | OpenSpec.tasks defines WHAT contract; writing-plans defines HOW execution; the latter consumes the former |
| Verification | OpenSpec.verify vs Superpowers.verification-before-completion | run both; see Verification Topology |
| Doc sedimentation | OpenSpec change docs vs RepoMem memory | OpenSpec is the authoritative source per change; RepoMem extracts durable lessons at archive time and never duplicates the change record |

## Verification Topology (Fix A3)

- OpenSpec.verify — answers "did we deliver what the spec promised?"
- Superpowers.verification-before-completion — answers "is the implemented behavior actually correct?"
- Both run before requesting-code-review.
- A change cannot enter finishing-a-development-branch unless both pass.

## Merge Gates (Fix A4)

- RepoMem.merge MUST run after OpenSpec.archive, never before.
- RepoMem.merge is HITL: human reviews promotion candidates before they enter the long-term layer.
- RepoMem.prune / split runs on a different cadence — periodic, not per-task.

## Suitability Envelope (Fix A5)

### Fits

- solo or small-team
- long-lived repositories
- changes can be sliced into discrete change units
- risk medium to high

### Does Not Fit

- pure spike / probe experiments (OpenSpec friction too high)
- short-lived repos (RepoMem overhead unjustified)
- multi-team large-scale coordination (needs a heavier primary workflow above this combo)

## Temporary Contractor Boundary Rules

### Temporary Contractor May Adjust

- choose lighter or heavier task-level flow by clarity and delivery target
- reduce OpenSpec intensity for tiny low-risk tasks
- raise or lower Superpowers intensity by task risk

### Temporary Contractor May Not Override

- the existence of OpenSpec, RepoMem, Superpowers as baseline
- long-term governance and safety constraints
- this document's collaboration-scale assumption without full rewrite
- Pipeline ordering, Merge Gate sequencing, or Verification Topology — these are recipe-level invariants. The temporary contractor MAY skip one only by declaring the exception in its `Recipe Invariant Exceptions` section, with reason and compensating action. Default is deny — silent skips are forbidden.

## Full Rewrite Conditions

- team shrinks to solo or grows into large-team conditions
- repository switches to a heavier coordination mode requiring a primary workflow
- default baseline changes the active layers materially

(Note: under add-only, switching to a superset recipe — e.g., adding ECC — is
an extension event, not a rewrite. Update `Recipe Reference` in place. The
add-only principle does not allow dropping a layer like OpenSpec, so "drop
OpenSpec" is not a valid event.)

## Related Documents

- docs/HarnessStack/temporary-<task>.md
- docs/RepoMem/persist/version-plan.md
- harness-stack/assets/templates/recipes/openspec-superpowers-repomem.md
