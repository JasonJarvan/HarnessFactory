# longterm.md — Superpowers-only example

> Worked example showing the long-term contract for a brand-new project with
> vague requirements that activates the `superpowers` recipe (single-layer).
> This is the asymmetric counterpart to
> `openspec-superpowers-repomem-longterm_orient.md` and stresses different
> template edges: Primary `none` plus three other inactive layers.

## Skill Inputs (declared)

- Layer choices (pre-fixed by user): Superpowers only
- Recipe matched: `superpowers`
- Implied scenario (per recipe Compatible Scenarios): scale stays open between
  solo and small-team; `Layer-First` flow asks the user. Example below
  picks small-team / product / short-lived / governance=disabled to show a
  scenario where most layers stay inactive.
- Output mode: Mode B (no existing `longterm.md`); no current task.

## Document Meta

- Repository: <target-repo>
- Effective From: 2026-05-07
- Source Template: harness-stack/assets/templates/longterm-template.md
- Recipe Reference: harness-stack/assets/templates/recipes/superpowers.md
- Last Updated Because: Initial baseline for a new vague-requirements project.

## Current Long-Term Assessment

- Collaboration Scale: small-team
- Repository Type: product
- Project Horizon: short-lived
- Long-Term Knowledge Governance: disabled

## Current Active Long-Term Baseline

### 1. Primary Workflow Layer

- Default enabled: none
- Emergent Ownership: Superpowers brainstorming and writing-plans carry
  primary workflow responsibility.
- Default inactive: BMAD, gstack, GSD
- Upgrade trigger:
  - changes start needing durable scope boundaries → add Spec layer
    (extend to `openspec-superpowers`)
  - cross-task coordination cost rises → add Primary framework layer

### 2. Spec Layer

- Default enabled: none
- Default inactive: OpenSpec
- Upgrade trigger: changes start needing durable scope boundaries

### 3. Execution Discipline Layer

- Default enabled: Superpowers
- Default inactive: none
- Upgrade trigger: raise verification and review intensity for risky work

### 4. Repository Memory Layer

- Default enabled: none
- Default inactive: RepoMem
- Upgrade trigger: project shifts from short-lived to long-lived; cross-task
  knowledge starts accumulating

### 5. Harness Enhancement Layer

- Default enabled: none
- Default inactive: ECC
- Upgrade trigger: agent context quality, safety, or repeatability becomes a
  recurring problem

## Pipeline

1. Superpowers.brainstorming — clarify vague intent
2. Superpowers.writing-plans — produce executable plan
3. Superpowers.using-git-worktrees + executing-plans + TDD — implement
4. Superpowers.verification-before-completion — verify behavior
5. Superpowers.requesting-code-review
6. Superpowers.finishing-a-development-branch

## Cross-Layer Conflicts

- N/A (single-layer recipe).

## Verification Topology

- Superpowers.verification-before-completion is the single verification entry
  before requesting-code-review.

## Merge Gates

- No cross-layer merge gate. Branch finishing is the only completion event.

## Suitability Envelope

### Fits

- brand-new projects with vague requirements
- solo or small-team
- exploration-first work where formal change specs would add friction

### Does Not Fit

- projects whose changes already need durable spec boundaries
- multi-team coordination

## Temporary Contractor Boundary Rules

### Temporary Contractor May Adjust

- raise or lower Superpowers intensity by task risk
- add OpenSpec, RepoMem, or ECC for the current task only when the change
  warrants it (note: under add-only, adding a layer once for a task creates
  pressure to upgrade the long-term recipe; record the trigger explicitly)

### Temporary Contractor May Not Override

- the existence of Superpowers as baseline
- Pipeline ordering and Verification Topology — recipe-level invariants;
  skipping requires an explicit declaration in the temporary contractor's
  `Recipe Invariant Exceptions` section

## Full Rewrite Conditions

- team grows into large-team conditions
- repository switches to a heavier coordination mode requiring a primary
  workflow

(Note: extending the recipe — e.g., `superpowers` → `openspec-superpowers` —
is an extension event, not a rewrite. Update `Recipe Reference` in place.)

## Related Documents

- docs/HarnessStack/temporary-<task>.md
- harness-stack/assets/templates/recipes/superpowers.md
