# longterm.md (raw skill output)

> This file is the raw result of running the `harness-stack` skill on the
> three-method combination `OpenSpec + Superpowers + RepoMem`.
> It is intentionally unmodified so problems are visible.
> The corrected version lives in `openspec-superpowers-repomem-longterm_orient.md`.

## Skill Inputs (declared)

- Layer choices (pre-fixed by user): `OpenSpec + Superpowers + RepoMem`
- Implied scenario (reverse-derived from layer choices):
  - Collaboration Scale: `small-team` (solo disables OpenSpec by default; large-team requires a Primary)
  - Repository Type: `product`
  - Project Horizon: `long-lived` (RepoMem only valuable when long-lived)
  - Long-Term Knowledge Governance: `enabled`
- Output mode: Mode B (no existing `longterm.md`); no current task, so no temporary contract.

## Document Meta

- Repository: <target-repo>
- Effective From: 2026-05-07
- Source Template: harness-stack/assets/templates/longterm-template.md
- Last Updated Because: Initial baseline using OpenSpec + Superpowers + RepoMem combination.

## Current Long-Term Assessment

- Collaboration Scale: small-team
- Repository Type: product
- Project Horizon: long-lived
- Long-Term Knowledge Governance: enabled

## Current Active Long-Term Baseline

### 1. Primary Workflow Layer

- Default enabled: none by default
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

## Temporary Contractor Boundary Rules

### Temporary Contractor May Adjust

- choose lighter or heavier task-level flow by clarity and delivery target
- reduce OpenSpec intensity for tiny low-risk tasks
- raise or lower Superpowers intensity by task risk

### Temporary Contractor May Not Override

- the existence of OpenSpec, RepoMem, Superpowers as baseline
- long-term governance and safety constraints
- this document's collaboration-scale assumption without full rewrite

## Full Rewrite Conditions

- team shrinks to solo or grows into large-team conditions
- repository switches to a heavier coordination mode requiring a primary workflow
- default baseline changes the active layers materially

## Related Documents

- docs/HarnessStack/temporary-<task>.md
- docs/RepoMem/persist/version-plan.md
