# 为什么需要 Agent Skills？——第 I 部分

## 课程文件

**初始对话：**以下是初始对话中使用的提示词和文件：

- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L1-partI/prompts_initial_conversation.md" target="_blank">prompts</a>
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L1-partI/campaign_data_week1.csv" target="_blank">CSV 文件</a>
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L1-partI/budget_reallocation_rules.md" target="_blank">预算重新分配规则</a>

**Skill 文件：**你可以在 <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L1-partI/skill/analyzing-marketing-campaign/" target="_blank">这里</a> 找到 `analyzing-marketing-campaign` skill 的文件。

**上传 skill 后的对话：**
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L1-partI/prompts_with_skills.md" target="_blank">prompts</a>
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L1-partI/campaign_data_week1.csv" target="_blank">CSV 文件</a>
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L1-partI/output_report_example/Marketing_Campaign_Report_Dec9-15.xlsx" target="_blank">拍摄过程中得到的 Excel 报告</a>

## 如何试用 Skills？

如果你没有 Claude 订阅，也仍然可以在 Claude.ai 的免费计划中试用该 skill（使用 Sonnet 4.5 或 Haiku 4.5）。截至 1 月 26 日，Claude.ai 的免费用户也可以使用 Skills。

由于 skills 是一个开放标准，你也可以在任何其他支持 skills 的 AI 应用中试用它们。你可以在 <a href="https://agentskills.io/home#adoption" target="_blank">这里</a> 找到支持的平台列表。

## 如何扩展 `analyzing-marketing-campaign` Skill？

你可以添加：
- 一个参考文件，说明如何分析并修复数据质量问题
- 一个参考文件，汇总你可能感兴趣的所有营销指标及其计算方式
- 基于这些数据还能做的更多分析
- 当未提供 CSV 时，如何从数据库查询数据的说明

也欢迎你结合自己的工作流一起思考：
- 是否有一些你会反复要求 agent 遵循的指令？
- 能否把它们整理成一个 skill？
- 是否有某些针对特定任务的指南，希望你的 agent 始终遵循？

**注意：**本课程展示的所有 skills 仅用于教学目的。每个展示的 skill 都有继续增强与迭代的空间。

## 参考资料

* <a href="https://agentskills.io/home" target="_blank">Agent Skills</a>
* <a href="https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview" target="_blank">Anthropic 文档：Agent Skills</a>
* <a href="https://claude.com/blog/skills" target="_blank">博客：Introducing Agent Skills</a>
