# 创建自定义 Skills

## 自定义 Skills 链接
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L4/custom_skills/analyzing-time-series/" target="_blank">analyzing time series</a>
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L4/custom_skills/generating-practice-questions/" target="_blank">generating practice questions</a>

## 参考资料
如需查看完整的创建 Skills 最佳实践与规范说明，请务必查看：
- <a href="https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices" target="_blank">Skill authoring best practices</a>
- <a href="https://agentskills.io/specification" target="_blank">Specification</a>

## 如何在 Claude Code 中禁用插件？

插件被设计为可按需启用/禁用。当你需要某些能力时启用，不需要时禁用，可以减少系统提示词的上下文内容与复杂度。

- 使用 `/plugin` 命令：进入 `installed` 选项卡，然后选择你想禁用的插件。
- 使用命令行：
`claude plugin disable <plugin-name>`

## 幻灯片内容总结

### SKILL.md 文件结构

一个 skill 文件主要包含两部分：
1. **YAML Frontmatter** —— 顶部元数据
2. **正文内容** —— 下方的 Markdown 指令

### Frontmatter 必填字段

| 字段 | 约束 |
|-------|-------------|
| **name** | 最多 64 个字符；只允许小写字母、数字和连字符；不能以连字符开头/结尾；必须与父目录同名；推荐使用动名词（动词+-ing）形式 |
| **description** | 最多 1024 个字符；不能为空；应描述 skill 做什么以及何时使用；包含具体关键词以帮助 agent 识别相关任务 |

### Frontmatter 可选字段

| 字段 | 约束 |
|-------|-------------|
| **license** | 许可证名称或指向许可证文件的引用 |
| **compatibility** | 最多 500 个字符；指明环境要求 |
| **metadata** | 任意键值对（例如 author、version） |
| **allowed-tools** | 预先批准的工具列表（以空格分隔，实验性） |

### 正文内容

**没有格式限制**，但这里有一些建议：

#### 推荐章节
- 分步骤说明
- 输入格式 / 输出格式 / 示例
- 常见边界情况

#### 实用建议
- 尽量 **控制在 500 行以内**
- 将详细参考资料拆到单独文件中（正文保留基础内容，并链接到更深入内容）
- references 尽量 **只比 SKILL.md 深一层**（避免嵌套引用）
- 表达清晰简洁，术语保持一致
- 文件路径使用正斜杠，即使在 Windows 上也是如此

#### 自由度（Degrees of Freedom）

| 等级 | 描述 |
|-------|-------------|
| **高自由度** | 通用的文字方向指引；允许多种有效做法 |
| **中等自由度** | 指令包含可定制的伪代码、代码示例或模式；存在推荐模式但可接受一定变化 |
| **低自由度** | 指令引用特定脚本；必须按特定顺序执行 |

#### 复杂工作流
- 将复杂操作拆解为清晰、连续的步骤
- 如果步骤很多导致工作流过大，考虑拆到独立文件中

### 可选目录

#### `/assets`
- **模板：**文档模板、配置模板
- **图片：**图表、logo
- **数据文件：**查找表、schema

#### `/references`
- 放置 agent 在需要时可阅读的额外文档
- 保持单个参考文件主题聚焦
- **注意：**对于超过 100 行的参考文件，建议在顶部添加目录，让 agent 能看到整体范围

#### `/scripts`
- 清楚说明依赖
- 脚本应有清晰文档
- 错误处理要明确且具备可读性
- **注意：**在指令中明确 Claude 应该执行脚本还是将其作为参考阅读

### 评估（Evaluation）

#### 单元测试

测试用例应定义：
- **skills**：需要测试哪些 skills
- **queries**：要运行的测试提示词
- **files**：要使用的输入文件
- **expected_behavior**：成功的判定标准

#### 示例测试用例
```json
{
  "skills": ["generating-practice-questions"],
  "queries": [
    "Generate practice questions from this lecture note and save it to output.md",
    "Generate practice questions from this lecture note and save it to output.tex",
    "Generate practice questions from this lecture note and save it to output.pdf"
  ],
  "files": ["test-files/notes.pdf", "test-files/notes.tex", "test-files/notes.pdf"],
  "expected_behavior": [
    "Successfully reads and extracts the input file. For pdf input, uses pdfplumber.",
    "Successfully extracts all the learning objectives.",
    "Generates the 4 types of questions.",
    "Follows the guidelines for each question.",
    "Uses the output structure and the correct output templates.",
    "The latex output successfully compiles.",
    "Saves the generated questions to a file named output."
  ]
}
```
**更多评估建议：**

- 获取**人工反馈**
- 用你计划使用的**所有模型**测试
