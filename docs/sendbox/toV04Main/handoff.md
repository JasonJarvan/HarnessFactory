# Handoff to V04 Main Session

**From**: 当前 v0.3.x 收尾 session
**To**: V04 main session（即将接手 v0.4 工作）
**Date**: 2026-05-15
**Repo**: `D:/Documents/Codes/Source_Jason/Tool_Dev/HarnessStack`
**Branch**: `master`（origin/master 落后 19 commits，未 push）

---

## 1. 你的主任务（v0.4）

在 `harness-factory/assets/templates/recipes/openspec-superpowers-repomem.md`
**同时**引入两块新章节（两轴必须同时设计，不可拆分）：

### A. Task-Level Document Partition（内容分区轴）

把 OSR+ECC kit 里"任务级文档三件套不得互相重复"的规则**从 kit 上抬到
recipe**。明确以下 6 份任务级文档各自的内容边界：

| 文档 | 拥有 | 排除 |
|---|---|---|
| OpenSpec `proposal.md` | WHY / WHAT scope | 实现路径 / 推理过程 |
| OpenSpec `design.md` | 对外可契约化的设计决策（接口、契约、合约级取舍） | 内部实现细节 |
| OpenSpec `specs/` + `tasks.md` | 已凝固的 spec 与执行步骤索引 | 草案、被否决方案 |
| RepoMem `requirement.md` | 调研过程、被否决方案、对话上下文 | 已 spec 化的 WHY |
| RepoMem `architecture.md` | 实现路径的 tacit 推理、被排除的实现细节 | 代码可推导的 HOW |
| Superpowers writing-plans `plan` | HOW 执行步骤 | WHY / 设计决策 |

**约束**：bare recipe（不附 OSR+ECC kit）的目标仓库也应能直接用这条规则。

### B. Task-End Disposition（处置判据轴）

新章节，给每个任务级文档/段落定义任务末三类处置：

- **archive**（`OpenSpec.archive`）：冻结为历史 spec 记录
- **merge → long-term**（`RepoMem.merge` HITL）：reviewer 判据表，至少含
  跨任务复用价值、决策耐久性、不与已 archive 重复、非代码可推导（tacit why）
- **burn**（任务结束即丢，**首次合法化**）：死胡同、被范围变更淘汰的中间态、
  完全被 archive 覆盖的内容；必须主动声明，避免默认全部 merge 造成长期记忆膨胀

**两轴必须同时设计**：分区不清楚 → 无法判处置；处置不清楚 → 分区只是装饰。

---

## 2. v0.4 开工前必谈（5 个 burn 未澄清点）

burn 是新引入概念，下列 5 点不拉齐，写出来的判据表就是占位：

1. **Default disposition**：默认 merge 还是默认 burn？（前者保旧行为；
   后者强制声明）
2. **Mandatory declaration**：burn 是否每一条都要显式声明？
3. **HITL 范围**：burn 是否也走 HITL，还是 author 单方决定？（merge 已确定走 HITL）
4. **判据边界**：什么算"被 archive 覆盖"、什么算"死胡同"——需要正反例
5. **审计痕迹**：burn 内容直接 delete，还是留 log / tombstone？

**这 5 点必须 brainstorming 与用户确认**（按 `superpowers:brainstorming` 流程），
不可直接写章节。

---

## 3. v0.3.x 已交付状态（你接手的起点）

### 最新 commits（origin/master 之后）

```
e9ad442 refactor(skill): v0.3.2 split add-only into two scopes
cb39e32 dogfood(v0.3.1): regenerate bundle + record validation conclusions
b542d85 feat(factory): v0.3.1 bundle trim + _toUser/ + {stack} path segment
e581457 dogfood(v0.3): run output pipeline + record discovered gaps  ← 这是 letter brief 引用的源头
```

### v0.3.1 核心变更（已 commit）

- bundle 形态收缩为 4 件：`README.md / longterm.md / temporary-<task>.md / _toUser/README.md`
- `_reference/` → `_toUser/` 改名；移除 `version-plan-skeleton.md`（target repo 自维护）
- 产物路径段 `{scale}-{horizon}` → `{stack}`（编码 active 层组成，
  如 `superpowers-repomem`、`openspec-superpowers-repomem-eccMedium`）
- 新增模板 `harness-factory/assets/templates/to-user-readme-template.md`
- `harness-factory/SKILL.md` 增 Step 11 渲染 `_toUser/README.md`；Output Rules 补
  "长期契约 landing 路径" 一句

### v0.3.2 核心变更（已 commit）

**add-only 原则降级**——这是你做 v0.4 时最重要的工具：

- **Target-Repo Scope（严格）**：目标仓库激活后，方法不脱活、recipe 升级走
  copy-on-write、`Recipe Reference` 单行替换；非可破例
- **Factory-Internal Scope（默认 + 显式破例）**：工厂内部对 recipe / 模板内容
  的修改/删除允许；破例必须在 recipe 的 `Last Updated Because` + commit
  message + （触及 load-bearing 规则时）version-plan 中声明

**v0.4 影响**：你**可以**直接精修 `openspec-superpowers-repomem.md` 的现有
Merge Gates / Cross-Layer Conflicts 条目（如果新章节迫使它们调整），不必绕道
新章节再 cross-ref 回去——但必须显式声明。letter brief 原文要求"必须遵守
add-only 原则"已经过时（letter brief 出自 v0.3 末，那时 add-only 还是 strict）。

### Dogfood 状态（已 commit）

`docs/HarnessStack/` 三件套已重生，type 改为 `platform`（备注：实际是
HarnessFactory skill，questionnaire 尚无 `skill` 枚举）。验证结论存于
`docs/RepoMem/persist/memory/harness-factory-v0.3.1-validation.md`。

**重要**：letter brief 原文说"不要直接改 docs/HarnessStack/longterm.md"，
这条仍然有效 —— 你修改的是 recipe 文件，不是 dogfood 激活态。recipe 改完
后，dogfood 不需要因为这次 recipe 变化而重生（v0.4 动的是
`openspec-superpowers-repomem.md`，dogfood 用的是 `superpowers-repomem.md`，
两者独立）。

---

## 4. 未结的轻量级 debt（不阻塞 v0.4，但记得带过去）

### a. v0.3.1 未验证：`{stack}` 真实 `output/` 渲染

dogfood 不走 `output/` 路径，所以 `{stack}` 段（含 `eccMedium` 等强度后缀
编码逻辑）从未被真实产线渲染过。**建议**：v0.4 收尾时跑一次真实 output（用
`openspec-superpowers-repomem-eccMedium` 这种复合 stack），顺手补这个验证。

### b. "无边界" 语义未澄清

用户在 v0.3.1 dogfood 启动时说"要求只有 superpowers+repomem，无边界"，
三种解读（无 Cross-Layer Conflicts / 无 Temporary Boundary Rules / 无
Suitability Envelope）未明确。当前按"不动 recipe-mandated 内容"保守处理。
v0.4 若涉及 boundary 类条目，**必须先问清**。

### c. v0.2 待办 bookkeeping

`version-plan.md § v0.2 待办` 列了 6 条，事实上 v0.3 / v0.3.1 阶段都已完成
但从未正式划掉。可在 v0.4 开工时顺手清账（或留作 v0.4.1 杂活）。

### d. v0.4 候选清单（除主任务 A/B 外）

- questionnaire `type` 引入 `skill` / `method` 枚举值（v0.3.1 dogfood 暴露）
- 模板渲染半自动化（当前 `output-readme-template.md` 与
  `to-user-readme-template.md` 手填 placeholder，无脚本）
- 调研层是否需要专门 skill（v0.3 第 4 条待办，仍未做）

**优先级**：以上都是子任务，**A + B 主目标先于这些**。

### e. Untracked artifact

`output/2026-05-15-1711-superpowers-repomem/` 是平行会话产物，未 commit。
里面 README 用 `<your-platform-repo>` 占位（疑似演示用）。**建议**：v0.4 决定
是否 commit 为参考样例、删除、或留 untracked 不处理。

### f. `docs/CN/` 中文镜像 freeze 在 v0.2

用户明确指示保留 v0.2 状态。v0.4 **不要**碰 `docs/CN/`，除非用户明确解锁。

---

## 5. 必读文件清单

按读取顺序：

1. `harness-factory/SKILL.md` —— 工厂 skill 入口（注意 v0.3.2 的双 scope
   add-only 段，整段重写过）
2. `harness-factory/assets/templates/recipes/openspec-superpowers-repomem.md`
   —— 你要改的 recipe
3. `harness-factory/assets/templates/recipes/openspec-superpowers-repomem-ecc.md`
   —— superset recipe，A/B 章节定型后可能需要同步
4. `harness-factory/references/selection-criteria.md § Authority By Field`
   + `§ Add-Only Constraint On Composition` —— Cross-Layer Conflicts 与
   Merge Gates 的权威性映射
5. `docs/RepoMem/persist/memory/cross-method-invariants.md` —— 跨方法不变量
   的现有积累（A 章节的输入素材）
6. `docs/RepoMem/persist/memory/harness-factory-v0.3.1-validation.md` ——
   v0.3.1 验证结论，含 5 个 v0.4 触发的回归条件
7. `docs/RepoMem/persist/version-plan.md` —— v0.3 / v0.3.1 / v0.3.2 全量记录
   与 v0.4 候选清单

---

## 6. 工作流约束（不变）

- 这是工厂仓库自身的变更，按现行 dogfood 契约执行（`docs/HarnessStack/longterm.md`）
  —— 主激活方法 RepoMem + Superpowers
- 用户偏好提问顺序：先模态后参数（见 auto-memory `feedback_question_ordering.md`）
- 设计阶段先 brainstorming（创意工作 → writing-plans 之前）
- 工厂改动走 brainstorming → spec → plan → implementation；
  **不直接热修**（letter brief 原话仍有效）

---

## 7. 不要做

- 不要碰 `docs/HarnessStack/longterm.md`（dogfood 激活态，与 recipe 改动是
  两件事；只有 recipe 改完且要重新激活才动）
- 不要碰 `docs/superpowers/specs/` 或 `docs/superpowers/plans/` 已存的
  2026-05-14 文件（时间戳历史）
- 不要碰 `docs/CN/`（freeze 在 v0.2）
- 不要把规则只写进 OSR+ECC kit —— v0.4 核心就是上抬到 recipe
- 不要默认所有任务级内容都 merge —— burn 是合法处置，本次的关键转变
- 不要把 `domain: harness-stack-execution-policy` 这类 frontmatter tag
  改名 —— 是制品域语义标识符，不是仓库名残留
- 不要在没问"5 个 burn 未澄清点"的情况下直接动笔写章节

---

## 8. 建议的首步动作

1. 读本 handoff 全文 + § 5 必读文件清单前 3 项
2. 跑 `git log --oneline -10` 与 `git status` 确认 working tree 干净
3. 用 brainstorming skill（`superpowers:brainstorming`）拉用户拉齐 5 个
   burn 未澄清点
4. brainstorming 收敛后，决定 A/B 是新章节、改既有条目、还是混合（v0.3.2
   降级后两种都允许，选最干净的）
5. 走 spec → plan → implementation；implementation 之前再次确认 commit 节奏
   （建议：A 一个 commit、B 一个 commit、可能 + 一个 superset sync commit）

---

## 9. 给 V04 session 的备忘

- **letter brief 比这份 handoff 旧**：你的用户给你看 letter brief 时，brief
  内容是 v0.3 末状态的快照。本 handoff 在 v0.3.2 之后写，反映最新进度。
  如果两者冲突，**以本 handoff 为准**。例如：letter 说"必须遵守 add-only
  原则"，handoff 说"add-only 已降级，可显式破例"——以 handoff 为准。
- **你不是 v0.3 收尾 session 的延续**：你是独立 session，从零开始，按本
  handoff + brief + repo 现状自行 onboard
- **如果发现 handoff 描述与 repo 实际不符**，以 repo 实际（git log + 文件
  内容）为准。本文档是 2026-05-15 时的快照
