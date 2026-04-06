# HarnessStack Output Shapes

## Purpose

Use this reference to keep outputs consistent after the question flow is complete.

## Output Modes

### Mode A: Temporary Contract Only

Use when:

- `docs/HarnessStack/longterm.md` already exists, and
- no long-term rewrite condition is triggered

Required outputs:

- one complete `docs/HarnessStack/temporary-<task>.md`

### Mode B: Long-Term Contract And Temporary Contract

Use when:

- `docs/HarnessStack/longterm.md` does not exist, or
- long-term rewrite conditions are clearly triggered

Required outputs:

- one complete `docs/HarnessStack/longterm.md`
- one complete `docs/HarnessStack/temporary-<task>.md` when there is a current task

### Mode C: Long-Term Rewrite Suggestion

Use when:

- current evidence suggests the long-term baseline may be wrong, but
- the information is not strong enough to rewrite it safely

Required outputs:

- a recommendation in conversation
- optionally a temporary contract for the current task

Do not silently rewrite `longterm.md` in this mode.

## Long-Term Output Shape

The generated `longterm.md` must contain:

1. source template and update metadata
2. long-term repository assessment
3. full active five-layer baseline
4. temporary contractor boundary rules
5. full rewrite conditions

## Temporary Output Shape

The generated `temporary-<task>.md` must contain:

1. task metadata
2. task assessment
3. adjustments relative to long-term baseline
4. final active five-layer stack
5. execution rules
6. conflict rules against long-term baseline
7. exit and merge rules

## Completeness Rules

- Write complete active documents, not pointers.
- Do not output only “use template X”.
- Do not leave key workflow layers implicit.
- If a layer is intentionally inactive, state that explicitly.
