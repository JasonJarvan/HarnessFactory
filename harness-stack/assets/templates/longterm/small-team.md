# longterm-small-team.md Template

## Document Meta

- Repository:
- Effective From:
- Source Template:
  - `harness-stack/assets/templates/longterm/small-team.md`
- Last Updated Because:

## Current Long-Term Assessment

- Collaboration Scale:
  - `small-team`
- Repository Type:
  - `product | research | platform | other`
- Project Horizon:
  - `short-lived | long-lived`
- Long-Term Knowledge Governance:
  - `enabled`

## Current Active Long-Term Baseline

### 1. Primary Workflow Layer

- Default enabled:
  - none by default
- Default disabled:
  - `BMAD`
- Upgrade trigger:
  - roadmap planning grows beyond lightweight coordination
  - cross-task coordination cost becomes persistently high

### 2. Spec Layer

- Default enabled:
  - `OpenSpec`
- Default disabled:
  - none by default
- Upgrade trigger:
  - enforce stronger use once collaboration drift appears

### 3. Execution Discipline Layer

- Default enabled:
  - `Superpowers`
- Default disabled:
  - none by default
- Upgrade trigger:
  - add stronger review, verification, and plan discipline for risky work

### 4. Repository Memory Layer

- Default enabled:
  - `RepoMem`
- Default disabled:
  - none by default
- Upgrade trigger:
  - split architecture and memory more aggressively as domains grow

### 5. Harness Enhancement Layer

- Default enabled:
  - `ECC(medium)`
- Default disabled:
  - none by default
- Upgrade trigger:
  - increase guardrails when shared context, safety, and repeatability become painful

## Temporary Contractor Boundary Rules

### Temporary Contractor May Adjust

- choose lighter or heavier task-level flow based on clarity and delivery target
- reduce `OpenSpec` intensity for tiny low-risk tasks
- increase `Superpowers` and `ECC` intensity for risky work

### Temporary Contractor May Not Override

- the existence of `OpenSpec`, `RepoMem`, or `Superpowers` as the team baseline
- long-term collaboration and governance rules
- this document's collaboration-scale assumption without full rewrite

## Full Rewrite Conditions

- team shrinks to solo or grows into large-team conditions
- repository shifts into much heavier coordination mode
- default baseline needs permanent heavier planning workflow

## Related Documents

- `docs/HarnessStack/temporary-<task>.md`
- `docs/RepoMem/persist/version-plan.md`
