---
name: harness-stack
description: Choose and generate long-term and temporary workflow contract documents for a repository using the HarnessStack model. Use when Codex needs to decide which workflow layers to activate for a project or task, create `docs/HarnessStack/longterm.md`, create `docs/HarnessStack/temporary-<task>.md`, or reconcile task workflows against a repository's long-term baseline.
---

# Harness Stack

## Overview

Use this skill to select and generate workflow contract documents for a repository.
The output is a long-term repository baseline and, when needed, a task-specific temporary contract that patches the baseline without rewriting it.

## Core Rules

- Treat `docs/HarnessStack/longterm.md` as the repository's complete long-term active contract.
- Treat `docs/HarnessStack/temporary-<task>.md` as the current task's complete temporary active contract.
- Do not make temporary contracts silently rewrite long-term governance.
- Do not copy the entire method repository into a target repository.
- In a target repository, `docs/HarnessStack/` should contain only active result documents.

## Workflow

1. Read repository context and current RepoMem facts when available.
2. Decide whether the repository needs a long-term baseline update or only a temporary task contract.
3. Read [references/selection-criteria.md](./references/selection-criteria.md) before choosing workflow layers, thresholds, or rewrite conditions.
4. Read [references/question-flow.md](./references/question-flow.md) before asking questions or deciding whether to emit long-term and temporary documents together.
5. Read [references/questionnaire.md](./references/questionnaire.md) to minimize and normalize the actual questions asked.
6. Read [references/output-shapes.md](./references/output-shapes.md) before generating final documents.
7. If generating a long-term contract, fill the template at `assets/templates/longterm-template.md`.
8. If generating a temporary contract, fill the template at `assets/templates/temporary-template.md`.
9. Keep long-term and temporary responsibilities separate:
   - long-term: stable baseline, boundaries, rewrite conditions
   - temporary: task assessment, task-level adjustments, final active stack
10. Write complete active documents, not template pointers or incomplete notes.

## Output Rules

- Prefer pure Markdown contractor documents first.
- If the repository already has a long-term contract, update it only when long-term conditions materially change.
- Otherwise, leave the long-term contract stable and generate only a temporary contract.
- Record contractor design decisions in RepoMem memory when they affect long-term governance.

## Resources

### assets/templates/

- `longterm-template.md`: Template for repository-level active long-term contract
- `temporary-template.md`: Template for task-level active temporary contract

### references/

- `selection-criteria.md`: Long-term and temporary decision factors, thresholds, and layer defaults
- `question-flow.md`: Compact question flow and output rules for generating active contractor documents
- `questionnaire.md`: Minimal question list and normalization rules
- `output-shapes.md`: Required output modes and completeness rules

Use these templates and references as the starting point for generated contract documents. Fill them with repository-specific results rather than copying method-repository metadata.
