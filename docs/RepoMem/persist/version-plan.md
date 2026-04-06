---
last_reviewed_at: 2026-04-04
---

# 版本计划

## 当前定位

当前仓库仍是工作流研究与内容聚合仓库，不是实际开发仓库的工作根目录。

当前已经确认的新方向：

- 这套多工作流契约体系的仓库名采用 `HarnessStack`
- 方法仓库的主要顶层目录采用 `docs/` 与 `harness-stack/`
- “可写入仓库的契约结果”第一阶段采用纯 Markdown
- 如果后续发现 agent 读取稳定性不足，再升级为 `Markdown + 极简机器可读清单文件`
- 目标开发仓库中的 `HarnessStack/` 目录只保存当前激活结果

## v0.2 目标

- 固化 `HarnessStack` 的仓库定位
- 将长期 contractor 与临时 contractor 的设计收敛为正式文档模板
- 在 `README.md` 中加入速查表与判断标准
- 在 `SKILL.md` 中加入问答式工作流选择逻辑
- 在 `harness-stack/` 中建立长期 contractor 与临时 contractor 的正式目录结构

## v0.2 待办

- 定义长期 contractor 的标准结构
- 定义临时 contractor 的标准结构
- 定义长期 contractor 与临时 contractor 的冲突优先级
- 定义 skill 的问答输入项与输出格式
- 定义 README 速查表的最短路径
- 将 `README.md` 改成真正的仓库首页说明

## v0.3 目标

- 将 contractor 体系转为可直接嵌入目标开发仓库的文档基线
- 让 skill 能基于仓库现状判断是否需要替换长期 contractor
- 让临时 contractor 明确描述如何嵌入当前长期 contractor
- 将根目录 `README.md` 改为正式 GitHub 首页说明

## v0.3 待办

- 验证纯 Markdown contractor 对 agent 的可读性是否足够稳定
- 如有必要，设计极简机器可读激活清单
- 验证 `RepoMem + contractor` 的长期协作方式

## 未来考虑

- 副标题与 GitHub 首页定位文案
- contractor 的英文实用文档版
- contractor 输出与真实开发仓库的激活方式
