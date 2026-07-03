# HarnessStack — `<target-repo>` at solo/long-lived

> One-time distillation source for an AI agent operating in the target
> repository. Read once, condense sections 1–4 into `CLAUDE.md`, then
> consult `longterm.md` for full detail. Re-read this file only on recipe
> upgrade.

## 1. Identity

This repository runs HarnessStack at `solo` scale, horizon `long-lived`, type `platform`.

- **Active recipe:** `superpowers-repomem-sendbox-dashboard`
- **Source template:** `harness-factory/assets/templates/longterm/solo.md`
- **Effective from:** `<YYYY-MM-DD>` (set on activation)

## 2. Active Methods

- `Superpowers` — execution discipline; brainstorming and writing-plans also carry the emergent primary-workflow responsibility (no separate Primary layer active).
- `RepoMem` — long-term repository memory (persist + temporary split, HITL merge into long-term).
- `sendbox-protocol` — file-based asynchronous channel for multi-session / cross-worktree coordination. Main agent's `docs/sendbox/` is the single source of truth; side cwds write to it by relative or absolute path.
- `cc-dashboard` — single-file projection of pending user actions at `docs/Dashboard/index.md`. Atomic granularity (one letter with N asks → N rows). Independent lifecycle from letters.
- Inactive by default: `OpenSpec` (spec layer), `ECC` / `ECC(light)` (harness enhancement, additional), `BMAD` / `gstack` / `GSD` (primary workflow frameworks).

## 3. Per-Task Pipeline (Compressed)

> This is the compressed view. **It is not authoritative.** For the full
> step list, conflict rules, and exception handling, see
> `longterm.md § Pipeline`. Sendbox letter writes and dashboard row writes
> are side-effects of the steps below, not separate steps.

1. `RepoMem.read` — load long-term architecture and memory as task context.
2. `Superpowers.brainstorming` — clarify vague intent. (Spawning a subagent here → write `handoff.md`; one dashboard row of type B.)
3. `RepoMem.capture` — open task-level temporary docs (requirement, architecture).
4. `Superpowers.writing-plans` — produce executable plan. (Subagent plan → `plan-ready.md`.)
5. Execute — `using-git-worktrees` + `executing-plans` + TDD; `RepoMem.capture` continuous. (A-12 boundary → blocker letter.)
6. `Superpowers.verification-before-completion` — single verification entry. (Subagent milestone → `milestone-done.md`.)
7. `Superpowers.requesting-code-review`. (Bundled `decisions.md` letters MAY be written here.)
8. `Superpowers.finishing-a-development-branch`. (`archived.md` MAY be written here.)
9. `RepoMem.merge` (HITL) — promote stable knowledge; any `promote-to-durable.md` content lands here.
10. `RepoMem.prune / split` — periodic hygiene, not per-task.

## 4. Hard Invariants

- **Add-only**: a method that has been activated never deactivates; upgrades are extensions, never replacements. Downgrades are NOT add-only — prefer leaving layers active-but-unexercised over removing them.
- **Single verification gate**: `Superpowers.verification-before-completion` MUST pass before `finishing-a-development-branch`. RepoMem, sendbox, and cc-dashboard have no verification role.
- **Merge ordering**: `RepoMem.merge` runs strictly AFTER `finishing-a-development-branch`, never before, and is always HITL. Any sendbox `promote-to-durable.md` content flows through this gate, never via a parallel path.
- **`<task>` = `<slug>`**: one identifier across RepoMem temporary docs and any HarnessStack temporary contract for the same task.
- **One sendbox per project**: the main agent's `docs/sendbox/` is canonical. Subagents in side cwds (`.worktrees/<task>/`, sibling repos, `/tmp/`) write to it by relative or absolute path — never fan out under their own cwd.
- **One letter → N dashboard rows**: each atomic user action emits its own row. Never collapse one letter to one row.
- **Sendbox and dashboard lifecycles are independent**: burning a letter does NOT cascade-delete dashboard rows; marking a row done does NOT trigger letter cleanup.
- **No content duplication across task-level documents**: writing-plans owns HOW; RepoMem temporary memory owns WHY/context. See `longterm.md § Cross-Layer Conflicts`.

## 5. Where To Read More

- Full long-term contract: `./longterm.md`
- Full usage manual (Day-One Init, per-task iteration, long-term iteration): `./_toUser/README.md`
- Task-level patch (if a task is in progress): `./temporary-<task>.md`

## 6. For AI Consumers

Distill sections 1–4 into `CLAUDE.md` (or the equivalent always-loaded
instruction file in your harness). Do not duplicate `longterm.md` verbatim;
the contract remains the authoritative source for details. Re-read this
README only on recipe upgrade or full rewrite events.
