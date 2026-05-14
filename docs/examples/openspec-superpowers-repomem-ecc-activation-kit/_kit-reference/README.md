# Activation Kit: openspec-superpowers-repomem-ecc

A ready-to-deploy artifact set for activating the
`openspec-superpowers-repomem-ecc` (OSR+ECC) recipe at small-team scale in a
target development repository.

Recipe definition:
[`harness-stack/assets/templates/recipes/openspec-superpowers-repomem-ecc.md`](../../../../harness-stack/assets/templates/recipes/openspec-superpowers-repomem-ecc.md)

---

## Kit Layout

```
openspec-superpowers-repomem-ecc-activation-kit/
├── longterm.md                            # core active contract
└── _kit-reference/
    ├── README.md                          # this file — kit usage manual
    └── version-plan-skeleton.md           # RepoMem version-plan template
```

| File | Purpose | Goes To |
|---|---|---|
| `longterm.md` | The long-term active contract | `<target-repo>/docs/HarnessStack/longterm.md` |
| `_kit-reference/version-plan-skeleton.md` | Multi-version roadmap skeleton (current detailed + future directional) | `<target-repo>/docs/RepoMem/persist/version-plan.md` (after rename + fill) |
| `_kit-reference/README.md` (this file) | Kit usage manual | stays inside `_kit-reference/`; not part of the target repo's active contract |

The kit's **core active contract** is `longterm.md` at the top level — copy
it as-is. Everything else is **reference material** for activation and lives
under `_kit-reference/`. The `_` prefix marks the directory as orthogonal to
the active contract; if you copy the entire kit into a target repo, the
`_kit-reference/` directory may stay alongside `longterm.md` as offline-readable
guidance or be deleted once activation is complete.

---

## Day-One Init In Target Repo

### Step 1 — Place the contract

Copy `longterm.md` to `<target-repo>/docs/HarnessStack/longterm.md`. Then fill
in the three TODO fields in `Document Meta`:

- `Repository`: target repo name
- `Effective From`: today's date
- `Repository Type`: pick one of `product | research | platform | other`

The other fields are determined by the recipe and should not be changed
without first reading `Full Rewrite Conditions`.

### Step 2 — Init the RepoMem long-term layer

Create the long-term knowledge skeleton:

```
<target-repo>/docs/RepoMem/persist/
├── architecture/    # stable architecture docs (one file per domain)
├── memory/          # cross-task memory (one file per topic)
└── version-plan.md  # multi-version roadmap (see below)
```

For `version-plan.md`, copy this kit's `version-plan-skeleton.md` and fill it
in. The skeleton organizes by version:

- **当前定位** — overall stage and target users
- **vX.Y 目标 / 待办** — detailed goals and work items for the current version
- **v(X.Y+1) 目标 / 待办** — directional goals for the next version
- **further versions** — direction only
- **未来考虑** — assumptions to validate, possible extensions

The version plan is the long-term roadmap source of truth; it carries forward
across tasks. When the current version closes, archive its work into
`architecture/` or `memory/` if any stable knowledge emerged, then promote
the next version from "next" to "current".

Each architecture / memory file should carry frontmatter:

```yaml
---
domain: <domain-name>
last_reviewed_at: <YYYY-MM-DD>
---
```

If you have a RepoMem skill, run its `init` command instead of creating
manually.

### Step 3 — Init OpenSpec

Follow OpenSpec's project setup to scaffold its change-tracking layout. The
contract assumes OpenSpec is reachable and that its commands
(`/opsx:explore`, `/opsx:propose`, `/opsx:apply`, `/opsx:verify`,
`/opsx:archive`) are usable from the agent harness.

### Step 4 — Confirm Superpowers skills

Confirm the agent harness can invoke at least these Superpowers skills:

- `brainstorming`
- `writing-plans`
- `using-git-worktrees`
- `executing-plans`
- `test-driven-development`
- `verification-before-completion`
- `requesting-code-review`
- `finishing-a-development-branch`

### Step 5 — Confirm ECC(medium) capabilities

ECC(medium) requires:

- a research-first MCP (Context7 or equivalent) for library/API docs
- cross-session memory persistence enabled in the harness
- team-shared skill discovery
- pre-commit hooks for format / lint / smoke evals
- a dependency security scan tool wired to fail builds on regression

If any are missing, either install them or temporarily switch
`Recipe Reference` to the leaner variant
`openspec-superpowers-repomem` until ECC is ready.

---

## Per-Task Iteration

Every task follows the 17-step pipeline in `longterm.md § Pipeline`. Concretely:

### Start of task

1. Pick the task identifier. The same string is used for the OpenSpec
   `change-id`, the RepoMem `<slug>`, and the HarnessStack `<task>` —
   `<task>` = `change-id` = `<slug>`. This is mandatory; see
   `longterm.md` § Task Identifier and Document Boundary.
2. Generate `<target-repo>/docs/HarnessStack/temporary-<task>.md` describing:
   - task name, scope, related change (using the identifier from step 1)
   - requirement clarity, delivery target, risk level
   - long-term knowledge impact
   - any `Recipe Invariant Exceptions` (must declare reason + compensating
     action; default is deny)
3. Run pipeline steps 1–8: research-first → RepoMem.read → brainstorming →
   OpenSpec.explore/propose → RepoMem.capture → writing-plans → execute →
   continuous capture. When calling RepoMem.capture and OpenSpec.propose,
   honor the per-task document boundary: change contract content goes to
   `openspec/changes/<id>/`; durable lessons and tacit knowledge go to
   `docs/RepoMem/temp/<slug>/`. Do not duplicate.

### During implementation

3. Continuous: `ECC.session-state.persist`, `RepoMem.capture` (tacit knowledge
   only — never duplicate OpenSpec change docs).

### Pre-completion

4. Run pipeline steps 10–13: pre-commit-eval → security-scan (if deps changed)
   → dual verification (OpenSpec.verify + Superpowers.verification-before-completion)
   → requesting-code-review.
5. Both verifications MUST pass before `finishing-a-development-branch`.

### Close-out

6. `Superpowers.finishing-a-development-branch` (step 14)
7. `OpenSpec.archive` (step 15) — security-scan must have passed if deps changed
8. `RepoMem.merge` (step 16, HITL) — human reviews promotion candidates before
   they enter the long-term layer. The reviewer MUST reject any temp content
   that duplicates the archived OpenSpec change record (delete, not merge).
   See `longterm.md` § Task Identifier and Document Boundary.
9. Retire `temporary-<task>.md` (delete or move to `temporary/archive/<task>.md`)

### Periodic (not per-task)

- `RepoMem.prune` and `RepoMem.split` run on a separate cadence (e.g., every
  N tasks or monthly).

---

## Long-Term Iteration

HarnessStack's recommended pattern is to extend methods rather than replace
them — the cognitive cost of swapping a method mid-project is high, so each
addition should be treated as a deliberate commitment. The target project
owns this decision; if you choose to remove a method, treat it as a project
decision and record the reason. This kit does not bind the project.

The default extension flow: switch `Recipe Reference` to a SUPERSET recipe and
re-render the five cross-layer sections from the new recipe.

| Trigger | Action | Rewrite needed? |
|---|---|---|
| ECC needs to go from medium to strong | switch Recipe Reference to an ECC(strong) superset recipe | No — extension event |
| Team grows past small-team | switch to a recipe with a primary workflow (`bmad-…` or `gsd-…` prefix); also bump `Collaboration Scale` to `large-team`, switch `Source Template` to `large-team.md` | Yes — scale change is a Full Rewrite condition |
| Project shrinks to solo | full rewrite required (scale change) | Yes |
| Need to add a primary workflow without scale change (rare) | extend Recipe Reference to a primary-bearing superset; record the trigger in `Last Updated Because` | No — extension event |
| Project becomes short-lived (rare) | full rewrite (horizon change) | Yes |

The `Full Rewrite Conditions` block in `longterm.md` is the canonical list.

---

## What Goes In `docs/HarnessStack/` In Target Repo

After Day-One Init plus a few task iterations, the target repo will look like:

```
<target-repo>/docs/HarnessStack/
├── longterm.md                     # the contract (this kit's artifact)
└── temporary-<task>.md             # current task's contract (one at a time, typically)
```

The method repo (`HarnessStack/`) is NEVER copied into the target repo. The
target repo only holds activated outputs.

---

## Reference

- Recipe definition:
  [`harness-stack/assets/templates/recipes/openspec-superpowers-repomem-ecc.md`](../../../harness-stack/assets/templates/recipes/openspec-superpowers-repomem-ecc.md)
- Parent recipe (OSR without ECC):
  [`harness-stack/assets/templates/recipes/openspec-superpowers-repomem.md`](../../../harness-stack/assets/templates/recipes/openspec-superpowers-repomem.md)
- Scenario subtemplate (small-team):
  [`harness-stack/assets/templates/longterm/small-team.md`](../../../harness-stack/assets/templates/longterm/small-team.md)
- Add-only principle: see `RepoMem` long-term decisions, item 7
