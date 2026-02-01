# 技能 vs 工具、MCP 与子代理

## 幻灯片内容总结

### Skills vs MCP

| 特性 | MCP | Skills |
|--------|-----|--------|
| **目的** | 将你的 agent 连接到外部系统与数据（数据库、API、服务） | 教会你的 agent 如何使用这些数据完成任务 |
| **示例** | MCP 服务器连接到数据库 | Skill 说明“用这张表的 A、B 列计算指标 X” |

MCP 提供*访问能力*，Skills 提供*专业知识*。

### Skills vs Tools

| 特性 | Tools | Skills |
|--------|-------|--------|
| **目的** | 为 agent 提供完成任务所需的基础能力 | 用专业知识扩展 agent 的能力 |
| **上下文** | 工具定义（name、description、parameters）始终存在于上下文窗口 | Skills 会按需动态加载 |
| **灵活性** | 固定的一组能力 | Skills 可以包含脚本，并在需要时作为工具使用（“按需工具”） |

### Skills vs Subagents

| 特性 | Subagents | Skills |
|--------|-----------|--------|
| **目的** | 具有隔离的上下文与工具权限 | 为主 agent 或任意子代理提供专业知识 |
| **运行方式** | agent 将任务委派给专门的子代理；子代理独立工作（可能并行）并返回结果 | Skills 指导工作应如何执行 |
| **示例** | 代码审查子代理 | 针对特定语言/框架的最佳实践 skill |

Skills 可以为主 agent **以及**它的子代理增强专业知识。

### 将它们组合起来

**示例：Customer Insight Analyzer（客户洞察分析器）**

| 组件 | 角色 |
|-----------|------|
| **Skill** | 指导如何对反馈进行分类、如何总结结论 |
| **MCP Server** | Google Drive MCP server 访问包含客户访谈笔记与问卷回复的 Drive 文件夹 |
| **Subagents** | Interview Analyzer、Survey Analyzer |

## 参考资料
* <a href="https://www.claude.com/blog/skills-explained" target="_blank">Skills Explained</a>
* <a href="https://support.claude.com/en/articles/12580051-teach-claude-your-way-of-working-using-skills" target="_blank">Teach Claude your Way of Working using Skills</a>
