---
domain: workflow-system
last_reviewed_at: 2026-04-04
---

# github-repo-design

## Constraints

- 当前 `CodingAgentHarnessSystem` 只是内容聚合仓库，不是实际开发仓库工作目录。
- 对外传播时，仓库名需要短、好记、易传播，不能过度暴露内部术语。
- 副标题尚未定稿，因此当前只固定主仓库名，不固定品牌口号。

## Decisions

- 当前这套多工作流契约体系的 GitHub 仓库名确定为 `HarnessStack`。
- `Harness` 用于强调“驾驭、编排、约束、驱动 agent/workflow 的运行方式”。
- `Stack` 用于强调“这是多层组合体系，而不是单一 workflow 或单一工具”。
- 当前阶段不急于确定副标题，避免过早冻结对外表述。
- 当前方法仓库的主要顶层目录收敛为 `docs/` 与 `harness-stack/`。
- `harness-stack/` 用于保存模板源、skill 内容与 contractor 方法定义。
- 目标开发仓库中的 `HarnessStack/` 目录只表示当前激活结果，不表示模板源。

## Rationale

- 与 `AgentStack` 相比，`HarnessStack` 更贴近当前仓库真正的内容深度：
  - workflow 组合
  - contract 层协调
  - RepoMem 记忆层
  - ECC harness 增强层
  - skill 问答选择
- `HarnessStack` 的传播性略弱于更泛化的名字，但表达准确性更高。
- 在副标题未定稿前，先固定主名，有利于后续目录、README 和 contractor 文档风格保持一致。

## Pitfalls

- `harness` 一词对部分 GitHub 路人有门槛，后续必须用副标题降低理解成本。
- 如果 README 首屏不清楚解释 “stack of workflows and contracts”，仓库定位会显得过于抽象。
- 如果方法仓库与目标开发仓库都使用 `HarnessStack` 名称，但不区分“模板源”和“激活结果”，读者和 agent 都会混淆。

## Related Memory

- 见 [workflow-system](./workflow-system.md)
- 见 [contractor-output](./contractor-output.md)
