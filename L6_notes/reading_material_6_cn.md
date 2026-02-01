# 使用 Claude Code 的 Skills

## 课程代码库与文件

课程文件链接：
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L6" target="_blank">课程中使用的代码库</a>
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L6/.claude/skills/" target="_blank">课程 skills 文件</a>
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L6/.claude/agents" target="_blank">子代理定义</a>
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L6_notes/prompts.md" target="_blank">对话中使用的 prompts</a>
- <a href="https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main/L6_notes/clear.py" target="_blank">clear.py</a>

当你第一次在终端运行应用时：
- 先执行 `uv sync`
- 激活虚拟环境：`source .venv/bin/activate`
- 试试以下命令：
   - `task –help`
   - `task add "write the final report" -p high -d 2025-01-15`
   - `task list`
   - `task done 1`
   - `task list -a`

这是一个 todo CLI 应用的 starter 代码库。在课程中，我们演示了如何添加 edit 和 clear 命令。你也可以通过添加 delete 和 undo 命令扩展该应用，或更改 tasks 的存储与展示逻辑。

## Claude Code

如果你是第一次尝试 Claude Code，可以看看这些课程：
- <a href="https://www.deeplearning.ai/short-courses/claude-code-a-highly-agentic-coding-assistant/" target="_blank">Claude Code：A Highly Agentic Coding Assistant</a>
- <a href="https://anthropic.skilljar.com/claude-code-in-action" target="_blank">Claude Code in Action</a>

如果你完成了这些课程，并希望看到更高级的 Claude Code 课程，请告诉我们你希望涵盖哪些主题。

如果你没有 Anthropic 订阅，也可以选择用 API key 运行 Claude Code。用 Sonnet 4.5 做同样练习的成本大约是 $1.57。

## 在 Claude Code 中使用 Skills

课程中你看到如何在项目级别添加 skills。这里还有一个<a href="https://code.claude.com/docs/en/skills#where-skills-live" target="_blank">列表</a>，说明 skills 还可以放在哪些位置。

### Frontmatter 还能添加哪些字段？

除了 `name` 与 `description`，在 Claude Code 中你还可以为 skills 添加多个字段，例如 `allowed-tools`、`model`、`disable-model-invocation`、`user-invocable`、`argument-hint`、`context` 和 `agent`。这些字段大多是在我们录制课程之后新增的，所以视频中没有机会覆盖。你可以在<a href="https://code.claude.com/docs/en/skills#frontmatter-reference" target="_blank">文档</a>中查看每个字段的说明。

### Claude Code 中的 Skills 调用方式

在 Claude Code 中，任何 skill 都可以由模型自动触发（课程中演示的方式），也可以由用户手动触发。例如，如果你想调用 `adding-cli-command` 这个 skill，你可以输入 `/adding-cli-command`，然后描述要添加什么命令。字段 `disable-model-invocation` 与 `user-invocable` 可进一步控制这种行为，详见<a href="https://code.claude.com/docs/en/skills#control-who-invokes-a-skill" target="_blank">文档</a>。

如果你发现 Claude Code 没有按预期调用 skill，请确认：
- 添加 skills 后已重启 Claude Code
- skill 的 description 足够具体，让 Claude 理解何时使用

你也可以随时手动调用 skill，或明确指示 Claude 使用某个特定 skill。

### Skills 与 Slash Commands 已合并

在 Skills 出现之前，Claude Code 有一个叫 slash commands 的功能：你可以在 `.claude` 下的 `commands` 文件夹中保存一个 Markdown 文件来创建自定义命令。

截至 1 月 23 日，自定义 slash commands 已并入 skills。原因是：`.claude/commands/review.md` 里的文件与 `.claude/skills/review/SKILL.md` 里的 skill 都会创建 `/review` 命令，且工作方式相同。不过 skills 还提供一些额外可选能力：用于放置支撑文件的专属目录（可在 `SKILL.md` 中引用），以及用于控制由你还是由 Claude 触发的 frontmatter 选项。

### 子代理与 Skills

课程中你看到如何创建自定义子代理。Claude Code 也内置了一些子代理，例如 `Explore`、`Plan` 与 `General-Purpose`（<a href="https://code.claude.com/docs/en/sub-agents#built-in-subagents" target="_blank">Built-in subagents</a>）。

使用 skills 搭配子代理有两种方式：

- **方式 1：**定义一个会使用 skills 的自定义子代理（课程中展示的方式）

    创建子代理时，你可以用 `skills` 字段在启动时把 skill 内容注入到子代理的上下文里。由于子代理不会继承父对话中的 skills，你必须显式列出 skills。子代理被调用时，`SKILL.md` 的完整内容会被注入到子代理的上下文中。

    `code-reviewer` 子代理的定义：
    ```
    ---
    name: code-reviewer
    description: "Reviews code for quality, security, and convention compliance. Use when user asks to review, check, or verify code"
    tools: Bash, Glob, Grep, Read
    model: inherit
    color: purple
    skills: reviewing-cli-command
    ---
    ```

    在这种情况下，`reviewing-cli-command` skill 对主 agent 和子代理都可用：主 agent 需要时可以加载该 skill，子代理被调用时也能以该 skill 指导审查流程。

    你也可以为 `code-reviewer` 子代理列出多个 skills。例如，再添加一个用于审查另一种语言/框架的 CLI 命令的 skill。或者添加一个用于审查 SQL 查询的 skill（如果你想把 tasks 存进数据库，而不是本地 JSON 文件）。

- **方式 2：**在子代理中运行 skills（课程未展示）

    如果你希望 skill 总是在隔离上下文中运行，需要在 skill 的 frontmatter 中使用 `context: fork`。skill 运行时，默认会由内置的 `general-purpose` 子代理接收该 skill 的内容作为 prompt 或任务，在隔离上下文中按指令执行，然后返回结果。如果你希望用某个特定子代理（内置或自定义）来执行 skill，需要在 skill 的 frontmatter 中指定 `agent` 字段。

    例如，下面是一个示例 `SKILL.md` 文件：
    ```
    ---
    name: deep-research
    description: Research a topic thoroughly
    context: fork
    agent: Explore
    ---

    Research $ARGUMENTS thoroughly:

    1. Find relevant files using Glob and Grep
    2. Read and analyze the code
    3. Summarize findings with specific file references
    ```

    参考：<a href="https://code.claude.com/docs/en/skills#run-skills-in-a-subagent" target="_blank">Run Skills in a subagent</a>

## 参考资料

- 更完整的 Claude Code Skills 使用指南：<a href="https://code.claude.com/docs/en/skills" target="_blank">documentation</a>
- Claude Code 子代理介绍：<a href="https://code.claude.com/docs/en/sub-agents" target="_blank">guide</a>
- <a href="https://code.claude.com/docs/en/skills#troubleshooting" target="_blank">Troubleshooting Guide</a>
