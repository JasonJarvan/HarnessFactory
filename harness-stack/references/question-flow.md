# HarnessStack Question Flow

## Purpose

Use this reference to run a compact question flow before generating contractor documents.

## Long-Term Questions

Ask these only when:

- the repository has no `docs/HarnessStack/longterm.md`, or
- there is evidence the long-term baseline may need a full rewrite

Recommended questions:

1. How many active contributors does this repository have?
2. Is this repository mainly a product, research, or platform repository?
3. Is this repository expected to be short-lived or long-lived?
4. Is there already a stable long-term workflow baseline in the repository?

## Temporary Task Questions

Ask these for the current task:

1. Is the requirement `clear`, `partially-clear`, or `vague`?
2. What is the delivery target?
3. What is the risk level?
4. Will this task produce knowledge that should likely persist beyond the task?

## Output Decision Rules

### Output Only Temporary Contract

Do this when:

- `docs/HarnessStack/longterm.md` already exists, and
- no long-term rewrite condition is triggered

### Output Long-Term Contract And Temporary Contract

Do this when:

- no `docs/HarnessStack/longterm.md` exists, or
- long-term rewrite conditions are triggered

### Output Long-Term Rewrite Suggestion Instead Of Rewrite

Do this when:

- the repository already has a stable long-term contract, and
- the evidence for rewrite is weak or incomplete

## Output Shape

For long-term output:

- produce a complete `docs/HarnessStack/longterm.md`
- include source template and current active baseline

For temporary output:

- produce a complete `docs/HarnessStack/temporary-<task>.md`
- include task assessment, adjustments, final active stack, and exit rules

For both:

- avoid template pointers
- avoid writing incomplete notes
- write final active contracts
