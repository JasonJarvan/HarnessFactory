# harness-stack

这个目录用于存放 `HarnessStack` 的方法源内容，包括：

- contractor 模板与结构约定
- skill 包内容
- 未来用于嵌入目标开发仓库的模板资源

当前规则：

- 当前 `HarnessStack` 仓库是方法仓库，不是目标开发仓库
- 因此这里保存的是模板源与方法定义，而不是某个业务仓库的激活结果
- 目标开发仓库中的 `HarnessStack/` 目录只应保存当前激活结果，不应混入模板库

当前阶段：

- 已确定 contractor 第一阶段使用纯 Markdown
- 已确定长期 contractor 与临时 contractor 分层
- 已确定目标开发仓库中的 `HarnessStack/` 是激活结果目录
- 已提供 `longterm.md` 与 `temporary-<task>.md` 的标准模板

当前模板：

- [longterm-template.md](/home/shenzhou/Codes/CodingAgentHarnessSystem/HarnessStack/harness-stack/assets/templates/longterm-template.md)
- [temporary-template.md](/home/shenzhou/Codes/CodingAgentHarnessSystem/HarnessStack/harness-stack/assets/templates/temporary-template.md)
- [longterm/solo.md](/home/shenzhou/Codes/CodingAgentHarnessSystem/HarnessStack/harness-stack/assets/templates/longterm/solo.md)
- [longterm/small-team.md](/home/shenzhou/Codes/CodingAgentHarnessSystem/HarnessStack/harness-stack/assets/templates/longterm/small-team.md)
- [longterm/large-team.md](/home/shenzhou/Codes/CodingAgentHarnessSystem/HarnessStack/harness-stack/assets/templates/longterm/large-team.md)
- [temporary/clear.md](/home/shenzhou/Codes/CodingAgentHarnessSystem/HarnessStack/harness-stack/assets/templates/temporary/clear.md)
- [temporary/partially-clear.md](/home/shenzhou/Codes/CodingAgentHarnessSystem/HarnessStack/harness-stack/assets/templates/temporary/partially-clear.md)
- [temporary/vague.md](/home/shenzhou/Codes/CodingAgentHarnessSystem/HarnessStack/harness-stack/assets/templates/temporary/vague.md)

相关长期记忆：

- [workflow-system architecture](/home/shenzhou/Codes/CodingAgentHarnessSystem/HarnessStack/docs/RepoMem/persist/architecture/workflow-system.md)
- [workflow-system memory](/home/shenzhou/Codes/CodingAgentHarnessSystem/HarnessStack/docs/RepoMem/persist/memory/workflow-system.md)
- [github-repo-design](/home/shenzhou/Codes/CodingAgentHarnessSystem/HarnessStack/docs/RepoMem/persist/memory/github-repo-design.md)
- [contractor-output](/home/shenzhou/Codes/CodingAgentHarnessSystem/HarnessStack/docs/RepoMem/persist/memory/contractor-output.md)
- [analysis](/home/shenzhou/Codes/CodingAgentHarnessSystem/HarnessStack/docs/analysis-lifecycle-workflow-comparison.zh-CN.md)
