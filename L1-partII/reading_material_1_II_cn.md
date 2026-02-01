# 为什么需要 Agent Skills？——第 II 部分

## 幻灯片内容总结

### 什么是 Agent Skills？

Agent Skills 是一种轻量级、开放的格式，用于扩展 AI agent 的能力。一个 skill 是一个包含有组织文件的文件夹，通常由指令、脚本、资产和资源组成，agent 可以发现并加载它们，从而更准确地完成特定任务。

### 我们过去如何看待 Agents

- 专业化 agent：研究 agent、编码 agent、金融 agent、营销 agent
- 每个 agent 都有自己狭窄的关注点、自己的脚手架，以及特定的工具

### 新范式

- **通用型 agent** 使用代码作为通用接口
- 简单脚手架：bash 与文件系统
- 但要可靠完成工作，它们仍然需要**上下文与领域专业知识**
- Skills 提供流程性知识，以及公司/团队/用户特定的上下文，让 agent 可按需加载

### Skills 能带来什么

| 类别 | 示例 |
|----------|----------|
| **领域专业知识** | 品牌指南与模板、法务审查流程、数据分析方法论 |
| **可复用的工作流** | 每周营销活动复盘、客户电话准备流程、季度业务复盘 |
| **新的能力** | 制作演示文稿、生成 Excel 或 PDF 报告、构建 MCP 服务器 |

### 没有 Skills 时

- 每次都要重新描述你的指令与需求
- 每次都要重新打包你的参考资料与支撑文件
- 需要人工确保工作流与输出始终一致

### Skills 的关键特性

1. **可移植（Portable）：**你可以在不同的 skills 兼容 agent 中复用同一个 skill：
    - Claude Code
    - Claude.ai
    - Claude Agent SDK
    - Claude API

    Agent Skills 现在是一个**开放标准**，正在被越来越多的 agent 产品采用。

2. **可组合（Composable）：**可以组合多个 skill 来构建复杂工作流。例如：
    - **公司品牌 skill**：提供品牌指南（字体、颜色、logo）
    - **PowerPoint skill**：生成幻灯片
    - **BigQuery skill**：提供与营销相关的 schema
    - **营销活动分析 skill**：分析营销数据

### Skills 如何工作？——渐进式披露（Progressive Disclosure）

Skills 可能包含大量信息，而且你可能拥有上百个 skill。为了保护上下文窗口，skills 采用**渐进式披露**：

| 层级 | 加载时机 |
|-------|-------------|
| **元数据**（YAML frontmatter：name、description） | 总是加载 |
| **指令**（主要的 SKILL.md 内容） | 触发时加载 |
| **资源**（参考文件、脚本） | 按需加载 |

### Skill 结构示例

根据 Agent Skills 规范：
- 必须包含 SKILL.md
- 可选目录：references、scripts 与 assets

由于一些 skill 在 Agent Skills 成为开放标准之前就已开发，你会看到某些 skill（例如下面的 PDF skill）并不严格遵循标准格式。
```
analyzing-marketing-campaign/
├── SKILL.md
└── references/
    └── budget_reallocation_rules.md
```
```
pdf/
├── SKILL.md
├── forms.md
├── reference.md
└── scripts/
    ├── check_fillable_fields.py
    ├── convert_pdf_to_images.py
    ├── extract_form_field_info.py
    └── fill_pdf_form_with_annotations.py
```
```
designing-newsletters/
├── SKILL.md
├── references/
│   └── style-guide.md
└── assets/
    ├── header.png
    ├── icons/
    └── templates/
        ├── newsletter.html
        └── layout.docx
```

## 参考资料

- <a href="https://agentskills.io/what-are-skills" target="_blank">What are Skills?</a>
- <a href="https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview#how-skills-work" target="_blank">How Skills Work</a>
- <a href="https://www.youtube.com/watch?v=CEvIs9y1uog" target="_blank">Barry Zhang & Mahesh Murag 在 AI Engineer's Fair 的分享</a>
