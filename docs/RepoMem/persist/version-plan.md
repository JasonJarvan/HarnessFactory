---
last_reviewed_at: 2026-05-14
---

# 版本计划

## 当前定位

当前仓库是 `HarnessFactory` —— 多工作流契约体系的**工厂仓库**，按用户引导
为每个目标仓库产出一份 `HarnessStack`（分层的 harness 配置）。仓库本身不
是任何具体业务仓库的工作根目录。

当前已确认：

- 仓库名 `HarnessFactory`，产出物名 `a HarnessStack`（每次产出 = 一份 HarnessStack）
- 方法仓库的主要顶层目录采用 `docs/`、`harness-factory/`、`output/`
- 产出物落到 `./output/{YYYY-MM-DD-HHmm}-{scale}-{horizon}/HarnessStack/`
- 目标开发仓库中的 `docs/HarnessStack/` 目录只保存当前激活结果
- contractor 第一阶段采用纯 Markdown；若 agent 读取稳定性不足，再升级为 `Markdown + 极简机器可读清单`

## v0.2 目标

- 固化 `HarnessFactory` 的仓库定位
- 将长期 contractor 与临时 contractor 的设计收敛为正式文档模板
- 在 `README.md` 中加入速查表与判断标准
- 在 `SKILL.md` 中加入问答式工作流选择逻辑
- 在 `harness-factory/` 中建立长期 contractor 与临时 contractor 的正式目录结构

## v0.2 待办

- 定义长期 contractor 的标准结构
- 定义临时 contractor 的标准结构
- 定义长期 contractor 与临时 contractor 的冲突优先级
- 定义 skill 的问答输入项与输出格式
- 定义 README 速查表的最短路径
- 将 `README.md` 改成真正的仓库首页说明

## v0.3 目标

- 完成 `HarnessStack` → `HarnessFactory` 仓库改名
- 完成 `harness-stack/` → `harness-factory/` 工厂源目录改名
- 引入产物结构 `./output/{run}/HarnessStack/`，固化目录与文件契约
- 引入产物顶层 README（AI 蒸馏入口），定义"压缩 Pipeline 不可成为权威"等防漂移约束
- `_kit-reference/` → `_reference/`，配套术语统一
- 清理 v0.2 之前的过期 examples 与 handoff 文档
- 在 RepoMem 中正式引入"调研层 / 推断层"工厂迭代分层概念
- 同步用户 auto-memory

## v0.3 待办

- 在真实目标仓库中跑一次产出流程，验证 `./output/<run>/HarnessStack/` 直接 copy 到 `docs/HarnessStack/` 可用
- 验证压缩 Pipeline 与 `longterm.md § Pipeline` 由同一 recipe source 渲染（不漂移）
- 验证 AI 在读完顶层 README 之后能正确蒸馏出 CLAUDE.md 内容
- 评估"调研层"是否需要专门 skill（v0.4 题）
- `harness-factory/SKILL.md § Output Rules` 增补一句：长期契约产物总是落在 `output/<run>/HarnessStack/longterm.md`（bundle 形式），与 README 同位；`docs/HarnessStack/` 仅在 dogfood 场景使用（2026-05-14 dogfood 测试中发现 Step 10 仅点名 README，未点名 longterm，落地依据只在 `references/output-shapes.md`）
- `_reference/README.md` 二选一并落定：补 `assets/templates/reference-readme-template.md` + 在 SKILL.md 加渲染步骤；或者从 `references/output-shapes.md` 的 bundle 图中移走，标为"目标仓库自维护，非工厂产物"

## 未来考虑

- 调研层的周期性 agent 化（v0.4+）
- 产出物的多人协作版本（多 stack 共存仓库的策略）
- contractor 输出的英文实用文档版
- （v0.4 候选）在 `openspec-superpowers-repomem` recipe 中同时引入**任务级文档分区**与**任务末处置判据**两块新章节——两轴必须同时设计，分区不清楚则无法判处置，处置不清楚则分区只是装饰：
  - **Task-Level Document Partition**：把 OSR+ECC kit `longterm.md § Task Identifier and Document Boundary` 的"三件套不得互相重复"规则上抬到 recipe Cross-Layer Conflicts，明确 `OpenSpec design.md` / `RepoMem architecture.md` / `RepoMem requirement.md` / writing-plans plan 之间的内容归属
  - **Task-End Disposition**：给 archive / `RepoMem.merge` / burn 三类处置写出 reviewer 判据表与 HITL 检查清单——把 `RepoMem.merge` 从"排序约束"升级为"带判据的过滤器"，并首次把 "burn" 作为合法且应主动声明的处置（防止默认全部 merge 造成长期记忆膨胀）
