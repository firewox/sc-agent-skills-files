# 使用 Claude API 的 Skills

## 课程文件

你可以在 <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L5" target="_blank">这里</a> 找到课程的 notebook 以及所有必需的输入文件。

要运行 notebook，你需要创建一个包含 Anthropic API key 的 `.env` 文件（不需要 Claude 订阅）：

`ANTHROPIC_API_KEY="your-key"`

你可以从 <a href="https://platform.claude.com/dashboard" target="_blank">Claude Developer Platform</a> 获取 key。

**关于成本：**请注意，把 notebook 的所有单元格完整跑一遍，大约会消耗 $0.67 的 API 额度。

如果你不想运行 notebook，你可以：
- 查看带有预运行输出的 <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L5/lesson_5.ipynb" target="_blank">notebook</a>（与视频中展示完全一致）
- 查看 <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L5/sample_outputs/" target="_blank">生成的示例输出</a>

你也可以在 Claude.ai 中试用同样的自定义 skills。

## 备注
- 这里是沙箱环境中<a href="https://platform.claude.com/docs/en/agents-and-tools/tool-use/code-execution-tool#pre-installed-libraries" target="_blank">预装库列表</a>
- Streaming：课程的 notebook 没有用 Messages API 实现 streaming。因此当你运行单元格获取响应时，可能需要等待几分钟。如果你想实现 streaming，可以查看<a href="https://platform.claude.com/docs/en/build-with-claude/streaming" target="_blank">文档</a>
- 若想查看更多使用 Agent Skills 搭配 API 的示例（例如多轮对话），请查看这份<a href="https://platform.claude.com/docs/en/build-with-claude/skills-guide" target="_blank">指南</a>

## 更多参考资料
- <a href="https://platform.claude.com/docs/en/agents-and-tools/tool-use/code-execution-tool" target="_blank">Code Execution Tool</a>
- <a href="https://platform.claude.com/docs/en/build-with-claude/files" target="_blank">Files API</a>
- <a href="https://github.com/anthropics/claude-cookbooks/tree/main/skills" target="_blank">Claude Cookbook：Skills</a>
