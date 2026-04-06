# longterm-solo.md Template

## Document Meta

- Repository:
- Effective From:
- Source Template:
  - `harness-stack/assets/templates/longterm/solo.md`
- Last Updated Because:

## Current Long-Term Assessment

- Collaboration Scale:
  - `solo`
- Repository Type:
  - `product | research | platform | other`
- Project Horizon:
  - `short-lived | long-lived`
- Long-Term Knowledge Governance:
  - `enabled | disabled`

## Current Active Long-Term Baseline

### 1. Primary Workflow Layer

- Default enabled:
  - none by default
- Default disabled:
  - `BMAD`
  - `gstack`
  - `GSD`
- Upgrade trigger:
  - repository enters long-lived roadmap-heavy mode
  - task portfolio becomes too large for execution-only discipline

### 2. Spec Layer

- Default enabled:
  - none by default
- Default disabled:
  - `OpenSpec`
- Upgrade trigger:
  - requirements need explicit change boundaries
  - delivery target reaches `MVP` or above
  - task risk or scope makes chat-only agreement unsafe

### 3. Execution Discipline Layer

- Default enabled:
  - `Superpowers`
- Default disabled:
  - none by default
- Upgrade trigger:
  - increase verification and review intensity when risk rises

### 4. Repository Memory Layer

- Default enabled:
  - `RepoMem` when repository is long-lived
- Default disabled:
  - `RepoMem` when repository is short-lived and disposable
- Upgrade trigger:
  - repository knowledge starts accumulating across tasks
  - architecture and decision memory need persistence

### 5. Harness Enhancement Layer

- Default enabled:
  - `ECC(light)` when memory, hooks, or verification loops are useful
- Default disabled:
  - `ECC`
- Upgrade trigger:
  - agent context quality, safety, or repeatability becomes a recurring problem

## Temporary Contractor Boundary Rules

### Temporary Contractor May Adjust

- add or skip `OpenSpec` for the current task
- raise or lower `Superpowers` intensity
- enable or disable lightweight `ECC` for the task

### Temporary Contractor May Not Override

- the existence of long-term repository memory once enabled
- long-term governance and safety constraints
- this document's collaboration-scale assumption without full rewrite

## Full Rewrite Conditions

- repository moves from solo to team collaboration
- repository becomes clearly long-lived after initially being short-lived
- default primary workflow needs to become permanently heavier

## Related Documents

- `docs/HarnessStack/temporary-<task>.md`
- `docs/RepoMem/persist/version-plan.md`
