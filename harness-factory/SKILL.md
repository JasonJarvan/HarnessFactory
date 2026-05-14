---
name: harness-factory
description: Choose and generate long-term and temporary workflow contract documents for a repository using the HarnessFactory model that generates HarnessStacks. Use when Codex needs to decide which workflow layers to activate for a project or task, create `docs/HarnessStack/longterm.md`, create `docs/HarnessStack/temporary-<task>.md`, or reconcile task workflows against a repository's long-term baseline.
---

# Harness Factory

## Overview

Use this skill to select and generate workflow contract documents for a repository.
The output is a long-term repository baseline and, when needed, a task-specific temporary contract that patches the baseline without rewriting it.

## Core Rules

- Treat `docs/HarnessStack/longterm.md` as the repository's complete long-term active contract.
- Treat `docs/HarnessStack/temporary-<task>.md` as the current task's complete temporary active contract.
- Do not make temporary contracts silently rewrite long-term governance.
- Do not copy the entire method repository into a target repository.
- In a target repository, `docs/HarnessStack/` should contain only active result documents.
- Long-term output may take one of two forms (chosen by the factory based on
  rendered length, per `references/output-shapes.md`):
  - Single file at `docs/HarnessStack/longterm.md`.
  - Index file at `docs/HarnessStack/longterm.md` plus extracted sections
    under `docs/HarnessStack/longterm/<section>.md`.

## Workflow

1. Read repository context and current RepoMem facts when available.
2. Decide whether the repository needs a long-term baseline update or only a temporary task contract.
3. Read [references/selection-criteria.md](./references/selection-criteria.md) before choosing workflow layers, thresholds, or rewrite conditions.
4. Read [references/question-flow.md](./references/question-flow.md) before asking questions or deciding whether to emit long-term and temporary documents together. Pick the entry mode (Scenario-First vs Layer-First) before asking anything.
5. Read [references/questionnaire.md](./references/questionnaire.md) to minimize and normalize the actual questions asked.
6. Read [references/output-shapes.md](./references/output-shapes.md) before generating final documents.
7. Pick a recipe from `assets/templates/recipes/` that matches the chosen
   layer combo. If none matches, draft a new recipe before continuing — do not
   bake inter-layer rules directly into the long-term contract.
8. If generating a long-term contract, fill the template at `assets/templates/longterm-template.md`. Copy Pipeline, Cross-Layer Conflicts, Verification Topology, Merge Gates, Execution Policy, and Suitability Envelope from the chosen recipe.
9. After filling the long-term template, count rendered lines and decide single-file vs index-plus-hooks per `references/output-shapes.md`. Emit the chosen form.
10. Render the top-level output README from
    `assets/templates/output-readme-template.md`, populating Identity,
    Active Methods, and the Compressed Pipeline from the same recipe used
    to fill `longterm.md`. The Compressed Pipeline (§3) MUST be derived from
    the recipe's Pipeline definition in one pass — do not author it
    independently of `longterm.md § Pipeline`. Place the rendered file at
    `<output>/HarnessStack/README.md`.
11. If generating a temporary contract, fill the template at `assets/templates/temporary-template.md`.
12. Keep long-term and temporary responsibilities separate:
    - long-term: stable baseline, boundaries, rewrite conditions, recipe binding
    - temporary: task assessment, task-level adjustments, final active stack
13. Write complete active documents, not template pointers or incomplete notes.

## Output Rules

- Prefer pure Markdown contractor documents first.
- If the repository already has a long-term contract, update it only when long-term conditions materially change.
- Otherwise, leave the long-term contract stable and generate only a temporary contract.
- Record contractor design decisions in RepoMem memory when they affect long-term governance.

## Add-Only Principle

- Once a method is activated for a project, it never deactivates. Upgrades are
  always additions, never replacements.
- Recipes follow the same rule via copy-on-write: extending a recipe means
  publishing a new file whose layer set is a superset of the previous one.
  The previous file is preserved.
- A long-term contract upgrades by switching its `Recipe Reference` to a
  superset recipe; this is an extension event and does NOT trigger a full
  rewrite review.

## Composition Rule

- Final activation = scenario × recipe, composed as `union`.
- See `references/selection-criteria.md` for the field-level authority table.

## Break-Glass For Recipe Invariants

- Pipeline ordering, Merge Gates, and Verification Topology are recipe-level
  invariants by default.
- A temporary contractor MAY skip one only by declaring the exception in its
  `Recipe Invariant Exceptions` section, with reason and compensating action.
  Default is deny — silent skips are forbidden.

## Resources

### assets/templates/

- `longterm-template.md`: Template for repository-level active long-term contract
- `temporary-template.md`: Template for task-level active temporary contract
- `output-readme-template.md`: Template for the top-level AI-distillation README placed at `<output>/HarnessStack/README.md`
- `longterm/`: Scenario subtemplates by collaboration scale (`solo`, `small-team`, `large-team`); each encodes scale-level defaults
- `temporary/`: Scenario subtemplates by requirement clarity (`clear`, `partially-clear`, `vague`)
- `recipes/`: Layer-combo recipes capturing Pipeline, Cross-Layer Conflicts, Verification Topology, Merge Gates, and Suitability Envelope. Final activation = scenario × recipe.

### references/

- `selection-criteria.md`: Long-term and temporary decision factors, thresholds, and layer defaults
- `question-flow.md`: Compact question flow and output rules for generating active contractor documents
- `questionnaire.md`: Minimal question list and normalization rules
- `output-shapes.md`: Required output modes and completeness rules

Use these templates and references as the starting point for generated contract documents. Fill them with repository-specific results rather than copying method-repository metadata.
