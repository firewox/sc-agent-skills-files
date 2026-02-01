# 使用 Claude Agent SDK 的 Skills

## 课程文件

你可以在 <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L7" target="_blank">这里</a> 找到 L7 的所有文件，其中包含一些与视频展示略有不同的地方：
- 每个子代理使用 `haiku` 作为模型
- 明确指定要使用的 MCP 工具列表

这里有一些值得探索的关键文件：
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L7/prompts" target="_blank">主 agent 与子代理的系统 prompts</a>
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L7/.claude/skills/learning-a-tool/" target="_blank">`learning-a-tool` skill 的文件</a>
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L7/utils.py" target="_blank">utils.py</a>（消息格式化）
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L7/agent.py" target="_blank">agent.py</a>
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L7_notes/learning-mineru/" target="_blank">拍摄过程中生成的学习指南</a>

要运行该 agent，请按 <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L7/README.md" target="_blank">README</a> 中的说明操作。你需要一个 Anthropic API key（不需要订阅）。

**关于成本：**如果子代理使用 `haiku`（主 agent 使用 `sonnet`），用相同请求运行该 agent 的成本大约是 &#36;3.43；如果子代理使用 `sonnet`，成本大约是 &#36;6.35。

### 课程中使用的 Prompts

**第 1 步：**启动研究流程
```
Help me get started with MinerU. Create a learning guide. Show me your plan first.
```

**注意：**该 agent 可能需要大约 15 分钟完成。你也可以更新 skill 的指令与 agent 定义，以获得更快的研究速度或更简化的学习指南。

**第 2 步：**审阅并批准计划

你可以同意计划，或提供你的反馈与建议。

**第 3 步（可选）：**导出到 Notion

如果你想试用与 Notion 的 MCP 集成：
```
Write ./learning-mineru/resources.md to the "Resources" subpage under Learning in Notion. The subpage already exists. Use rich formatting. For Notion MCP: You can use the full range of Notion block types for proper formatting.
```

**注意：**在课程使用的 Notion 账号中，我们创建了一个名为 `Learning` 的页面，并在其下创建了名为 `Resources` 的子页面。

## 更高级选项

- <a href="https://platform.claude.com/docs/en/agent-sdk/python#example-advanced-permission-control" target="_blank">高级权限控制</a>
- <a href="https://platform.claude.com/docs/en/agent-sdk/python#building-a-continuous-conversation-interface" target="_blank">构建持续对话界面</a>（中断、新对话、退出）

## 参考资料

- <a href="https://platform.claude.com/docs/en/agent-sdk/overview" target="_blank">Claude Agent SDK Documentation</a>
- <a href="https://platform.claude.com/docs/en/agent-sdk/python" target="_blank">Python Agent SDK</a>
- <a href="https://platform.claude.com/docs/en/agent-sdk/skills" target="_blank">SDK 中的 Agent Skills</a>
- <a href="https://github.com/anthropics/claude-agent-sdk-demos" target="_blank">Claude Agent SDK Demos</a>
