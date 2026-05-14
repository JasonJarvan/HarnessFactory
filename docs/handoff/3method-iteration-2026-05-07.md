# Handoff — HarnessStack 3-Method Recipe Iteration (2026-05-07)

> Temporary handoff document. Captures the conclusions, arguments, and
> information produced during the 2026-05-07 iteration on the
> `OpenSpec + Superpowers + RepoMem` (OSR) recipe. Intended for another AI
> session to read as context and either verify, extend, or build on this
> work.
>
> Status of changes: ALL listed conclusions have already been applied to the
> repository in this same session. Treat this doc as a record + audit trail,
> not a to-do list. The pending items at the bottom are explicitly deferred.

---

## 1. Background

- HarnessStack is a method repo for coding agent contractor workflows. It is
  not a target dev repo; it produces `longterm.md` and `temporary-<task>.md`
  contractor documents that target dev repos activate.
- The iteration started from the user's request to polish the
  `OpenSpec + Superpowers + RepoMem` (OSR) combination, then evolved into a
  structural refactor of the contractor model.

---

## 2. Conclusions Reached

### 2.1 Recommended single method for new + vague-requirements projects

- Pick **Superpowers**. GSD is the close runner-up.
- Reasoning:
  - Vague requirements → exploration-first; Superpowers' `brainstorming` skill
    is purpose-built for clarifying vague intent.
  - Brand-new project → no longterm baseline exists; heavy spec/memory layers
    are premature.
  - Superpowers' chain (`brainstorming` → `writing-plans` → `TDD` →
    `verification` → `finishing`) bridges vague-to-executable cleanly.
- Upgrade triggers (under add-only):
  - first edge-clear change → ADD OpenSpec (extend to `openspec-superpowers`)
  - PoC graduates to long-lived → ADD RepoMem
  - team crosses small-team threshold → ADD a Primary framework (BMAD)
- Important: triggers are ALL add-only. There is no "replace" path.

### 2.2 Recipe abstraction is needed

- The original template treated the 5 layers (Primary / Spec / Execution /
  Memory / Harness) as independent toggles. That shape lost inter-layer
  pipeline, conflicts, verification topology, and merge-gate semantics.
- Scenario subtemplates (`solo`, `small-team`, `large-team`) silently embedded
  implicit layer combos. Same combo at different scales produced different
  contracts even when the user wanted the combo to be the invariant.
- Resolution: split into two orthogonal axes.
  - **Scenario** = scale-level defaults (which methods are typical at this
    scale)
  - **Recipe** = layer combo + inter-layer rules (Pipeline, Cross-Layer
    Conflicts, Verification Topology, Merge Gates, Suitability Envelope)
- Final activation = scenario × recipe.

### 2.3 Add-only principle (固化 in project_decisions.md item 7)

- Once a method is activated for a project, it never deactivates.
- All upgrades are additions, never replacements. Method overlap is accepted
  as the cost.
- First activation must be deliberate — it is a permanent commitment.
- Direct consequences applied:
  - Vocabulary: `Default disabled` → `Default inactive` (binary
    Active/Inactive only; no permanent-exclusion state).
  - Recipe lifecycle: copy-on-write (see 2.4).
  - "Replace recipe" is not a valid event; only "extend to a superset recipe"
    exists.
  - The `the recipe is replaced` line was removed from
    `Full Rewrite Conditions`.

### 2.4 Recipe lifecycle = copy-on-write

- Recipes are immutable once published.
- Extending a recipe means publishing a new file whose layer set is a
  **superset** of the previous one. The previous file stays in place forever.
- Long-term contracts upgrade by changing their `Recipe Reference` to the new
  superset recipe; this is an **extension event**, not a rewrite event. Do
  not trigger a full rewrite review.
- Recipe naming convention: layer-canonical-order
  (Primary → Spec → Execution → Memory → Harness), lowercase
  hyphen-separated.
  - `superpowers.md` (Execution only)
  - `openspec-superpowers.md`
  - `openspec-superpowers-repomem.md`
  - `openspec-superpowers-repomem-ecc.md`
  - `bmad-openspec-superpowers-repomem-ecc.md`

### 2.5 Break-glass for recipe invariants

- Pipeline ordering, Merge Gates, and Verification Topology are recipe-level
  invariants — they encode the cross-layer guarantees that make a combo work.
- Default policy: **deny silent skips**. A temporary contractor MAY skip one
  invariant only by declaring the exception in its
  `Recipe Invariant Exceptions` section, with reason and compensating action.
- Skipping does NOT auto-trigger a longterm baseline review.
- Reasoning: hard-locking these invariants would leave no escape hatch for
  emergency fixes; allowing silent skips would erode the combo's correctness
  guarantees. Declaration-with-rationale balances both.

### 2.6 Composition rule

- Final activation = scenario × recipe, composed as `union` (per add-only).
- Authority by field:
  - `Document Meta`: skill at generation time
  - `Current Long-Term Assessment`: scenario
  - per-layer fields (Default enabled / Default inactive / Upgrade trigger /
    Emergent Ownership): recipe (scenario contributes only when recipe leaves
    a layer unspecified)
  - Pipeline / Cross-Layer Conflicts / Verification Topology / Merge Gates /
    Suitability Envelope: recipe (copy verbatim)
  - Boundary Rules / Full Rewrite Conditions: union of scenario and recipe;
    on overlap the stricter rule wins
- When scenario and recipe disagree on whether a layer is Active, recipe
  wins; report the conflict to the user — usually it means a different
  recipe should be picked.

### 2.7 Layer-First ambiguity rule

- When the user pre-fixes layer choices, the skill enters Layer-First mode.
- For each scenario axis (scale / type / horizon / governance):
  - if the matched recipe's `Compatible Scenarios` fix the axis to a single
    value, adopt silently
  - if the axis still has multiple compatible values, ask the user
- `Delivery Target` and `Risk Level` are always asked — never implied by
  layer choices.

### 2.8 Single-method recipe published

- `recipes/superpowers.md` is the canonical add-only starting point.
- Worked example: `docs/examples/superpowers-only-longterm.md`.

### 2.9 Delivery Target Compatibility added to recipes

- Each recipe must declare which delivery targets it suits and which it does
  not. Uses the questionnaire's normalized values:
  `<3h test | PoC | Demo | MVP | Alpha | Beta | MMP | RC | GA`.

### 2.10 Decisions deliberately NOT taken (to avoid premature complexity)

- `Emergent Ownership` is free-form text. No controlled vocabulary yet.
- `Recipe Invariant Exception` skips do not auto-trigger longterm review yet.
- Three-state activation (`Active` / `Available` / `Permanently excluded`)
  rejected in favor of binary `Active` / `Inactive`.

---

## 3. Arguments / Evidence

### 3.1 Original problems found by sampling OSR generation

| Code | Problem |
|---|---|
| A1 | Pipeline semantics absent from template |
| A2 | Cross-layer conflicts have no slot |
| A3 | Verification topology compressed into Execution layer |
| A4 | Merge gate timing missing |
| A5 | Suitability envelope missing |
| B1 | Layer-first entry mode missing from question flow |
| B2 | Same combo varies across scales |
| B3 | Generated OSR was 95%-identical to small-team.md (ECC delta) |
| C1 | Primary `none` slot is structurally ambiguous |

### 3.2 New problems surfaced while applying fixes

- **Dangling pointers**: solo.md and small-team.md reference recipes that
  don't yet exist (`superpowers-only`, ECC-bearing small-team recipe).
- **Two-sources-of-truth**: scenario subtemplates duplicate inter-layer rules
  that now also live in recipes. Drift risk.
- **Composition algorithm undefined** (resolved in 2.6).
- **Layer-First ambiguity unresolved** (resolved in 2.7).
- **Delivery target dimension absent** (resolved in 2.9).
- **`Default disabled` vocabulary collides with add-only** (resolved in 2.3).
- **`recipe is replaced` rewrite trigger collides with add-only** (resolved
  in 2.3).
- **`Recipe Invariant May Not Override` was too rigid** (resolved in 2.5).

---

## 4. Files Changed / Created

### 4.1 Created

- `harness-stack/assets/templates/recipes/recipe-template.md`
- `harness-stack/assets/templates/recipes/openspec-superpowers-repomem.md`
- `harness-stack/assets/templates/recipes/superpowers.md`
- `docs/examples/openspec-superpowers-repomem-longterm.md` (raw skill output)
- `docs/examples/openspec-superpowers-repomem-longterm_orient.md`
  (manually-patched fix demo)
- `docs/examples/superpowers-only-longterm.md` (asymmetric counterpart)
- `docs/RepoMem/persist/memory/template-evolution.md`
- `docs/handoff/3method-iteration-2026-05-07.md` (this file)

### 4.2 Modified

- `harness-stack/assets/templates/longterm-template.md`
  - added `Recipe Reference`, `Emergent Ownership`, 5 cross-layer sections
  - renamed `Default disabled` → `Default inactive`
  - softened boundary rule for break-glass
  - removed `the recipe is replaced` rewrite condition; added add-only note
- `harness-stack/assets/templates/temporary-template.md`
  - added `Recipe Invariant Exceptions` section
- `harness-stack/assets/templates/longterm/{solo,small-team,large-team}.md`
  - added Recipe Reference, Emergent Ownership, 5 cross-layer sections
  - renamed `Default disabled` → `Default inactive`
- `harness-stack/assets/templates/recipes/recipe-template.md`
  - added Naming Convention, Lifecycle, Delivery Target Compatibility
- `harness-stack/assets/templates/recipes/openspec-superpowers-repomem.md`
  - added Delivery Target Compatibility
- `harness-stack/references/question-flow.md`
  - added Entry Modes, Layer-First ambiguity rule
- `harness-stack/references/questionnaire.md`
  - added Q0 (entry-mode switch)
- `harness-stack/references/selection-criteria.md`
  - added Scenario × Recipe Composition section
- `harness-stack/SKILL.md`
  - added Add-Only Principle, Composition Rule, Break-Glass sections
  - workflow expanded with recipe-selection step

---

## 5. Pending Items (deliberately deferred)

1. **ECC-bearing small-team recipe** — `small-team.md` references it as
   default but the file does not exist. Build it before users adopt the
   small-team baseline. Suggested name:
   `openspec-superpowers-repomem-ecc.md`.
2. **Two-sources-of-truth** between scenario subtemplates and recipes. Each
   scale should eventually delegate inter-layer rules entirely to its default
   recipe. Until then, treat any change in inter-layer rules as a signal to
   extract or update a recipe.
3. **CN mirror under `docs/CN/`** has not been updated. Defer until the
   recipe abstraction stabilizes.
4. **README.md** still uses old Linux absolute paths (project moved to
   Windows). v0.2 to-do.

---

## 6. How To Use This Document

- For a fresh AI session: read sections 1, 2, and 3 to acquire the model and
  reasoning before touching any file.
- For verification: re-read each conclusion in section 2 and confirm the
  corresponding files in section 4 are coherent. The current session already
  applied the changes; if anything is missing, that is a real gap.
- For continuation: pick from section 5. Do NOT re-derive or re-apply
  anything in section 4 — it is already in the repo.

---

## 7. Worked Examples (currently in repo)

- `docs/examples/openspec-superpowers-repomem-longterm.md` — raw skill output
  before the fixes (kept on purpose to show the original problems)
- `docs/examples/openspec-superpowers-repomem-longterm_orient.md` —
  manually-patched version with each fix labeled (A1–A5, B1–B2, C1)
- `docs/examples/superpowers-only-longterm.md` — asymmetric counterpart for
  the single-method recipe
