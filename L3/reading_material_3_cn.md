# 探索预构建技能

## 预构建技能

* <a href="https://github.com/anthropics/skills/tree/main/skills" target="_blank">Anthropic skills 列表</a>
* <a href="https://github.com/anthropics/skills/tree/main/skills/pptx" target="_blank">pptx</a>
* <a href="https://github.com/anthropics/skills/tree/main/skills/skill-creator" target="_blank">Skill creator</a>

## 第 1 部分：更新营销 Skill

在视频中，我们更新了 Marketing skill，让它通过 BigQuery MCP server 从 BigQuery 表中获取数据，而不是要求提供 CSV 文件：

- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L3/prompts.md#part-1-updating-the-marketing-skill" target="_blank">第 1 部分使用的 prompts</a>
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L3/updated_marketing_skill/analyzing-marketing-campaign/" target="_blank">拍摄过程中得到的 Marketing skill 更新版文件</a>

你可以创建一个 BigQuery 表来尝试这一部分（说明链接见下方），也可以改为搭建本地数据库。例如，你可以搭一个本地 SQLite 数据库，把这个 <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L3/campaign_performance_4weeks.csv" target="_blank">CSV 文件</a> 导入数据库，然后使用这个 <a href="https://github.com/modelcontextprotocol/servers-archived/tree/main/src/sqlite" target="_blank">MCP server</a>。或者你也可以完全跳过这一部分。

- 可选：<a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L3/additional_references/table_setup.md#bigquery-setup" target="_blank">搭建 BigQuery 表的说明</a>
- 可选的替代方案：<a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L3/additional_references/table_setup.md#sqlite-setup" target="_blank">搭建 SQLite 表的说明</a>

**注意**：由于 BigQuery MCP Server 是本地 MCP server，我们使用的是 Claude Desktop（不是 Claude.ai）。在 Claude.ai 中，你只能使用远程 MCP servers。

## 第 2 部分：创建品牌指南 Skill

- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L3/brand_guidelines_files/" target="_blank">品牌指南文件</a>
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L3/prompts.md#part-2--creating-the-brand-guideline-skill" target="_blank">第 2 部分使用的 prompts</a>
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L3/brand_guidelines_skill/craftedwell-brand/" target="_blank">拍摄过程中得到的 skill 文件</a>

## 第 3 部分：实现完整工作流

- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L3/prompts.md#part-3-implementing-the-entire-workflow" target="_blank">第 3 部分使用的 prompts</a>
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L3/output_report_example/CraftedWell_Weekly_Report_Dec16-22.pptx" target="_blank">拍摄过程中得到的幻灯片</a>

这些幻灯片可能需要几分钟生成，并且外观可能与视频中的示例完全不同。
