# Agent Skills 深度技术分享 PPT 大纲与逐字稿

**时长**：30 分钟
**页数**：18 页
**目标受众**：技术团队、架构师、AI 开发者
**核心目标**：全面理解 Agent Skills 架构、生态定位及实战落地

---

## PPT 大纲概览

| 页码 | 模块 | 标题 | 核心内容 | 预估时长 |
| :--- | :--- | :--- | :--- | :--- |
| **P1** | 开场 | 封面：Agent Skills 技术详解 | 标题、演讲者 | 0.5 min |
| **P2** | 目录 | 今日议程 (Agenda) | 四大模块：概念、架构、生态、实战 | 0.5 min |
| **P3** | 背景 | Agent 范式的演进 | 从“专用 Agent”到“通用 Agent + 技能” | 1.5 min |
| **P4** | 概念 | 什么是 Agent Skills？ | 定义、核心特性（可移植、可组合） | 1.5 min |
| **P5** | 价值 | 为什么我们需要 Skills？ | 解决 Context Window 瓶颈，复用隐性知识 | 1.5 min |
| **P6** | 架构 | 核心机制：渐进式披露 | Progressive Disclosure / Lazy Loading 理念 | 2 min |
| **P7** | 架构 | 详解：三层加载模型 | Metadata (L1) -> Instructions (L2) -> Resources (L3) | 2 min |
| **P8** | 架构 | 运行环境：VM 与文件系统 | 安全沙箱、文件持久化、代码执行 | 1.5 min |
| **P9** | 生态 | 辨析：Skills vs MCP | 知识 (Expertise) vs 连接 (Access) | 2 min |
| **P10** | 生态 | 辨析：Skills vs Tools/Subagents | 流程指导 vs 原子能力 vs 独立任务 | 1.5 min |
| **P11** | 开发 | Skill 的解剖学 | 目录结构、YAML Frontmatter 规范 | 2 min |
| **P12** | 开发 | Context Engineering 最佳实践 | 500行原则、自由度控制 (Degrees of Freedom) | 2 min |
| **P13** | 开发 | 质量保证：测试与评估 | 单元测试策略、Eval 案例 | 1.5 min |
| **P14** | 实战 | 现成资源：Pre-Built Skills | Anthropic 官方库、skill-creator、pptx skill | 1.5 min |
| **P15** | 实战 | 案例 1：市场分析 (Skill + MCP) | 结合 BigQuery MCP 动态获取数据 | 2 min |
| **P16** | 实战 | 案例 2：品牌指南 (Brand Guidelines) | 管理静态资产、Logo、设计规范 | 2 min |
| **P17** | 实战 | 案例 3：完整工作流编排 | 多 Skill 协同：数据 -> 分析 -> 报告 | 3 min |
| **P18** | 总结 | 总结与行动建议 | 核心回顾、下一步计划 | 1.5 min |

---

## 详细汇报脚本

### P1: 封面
**【PPT内容】**
- **主标题**：Agent Skills 技术详解
- **副标题**：构建模块化、可扩展的 AI Agent 智能体系统
- **演讲者**：[你的名字]

**【演讲脚本】**
大家好，感谢大家参加今天的技术分享。
今天我们要深入探讨一个非常关键的技术——**Agent Skills**。随着 AI Agent 在业务中的应用越来越深，我们发现单纯靠 Prompt Engineering 已经很难维护复杂的业务逻辑。Agent Skills 提供了一套标准化的解决方案，让我们可以像管理代码模块一样管理 Agent 的能力。
接下来的 30 分钟，我将分 18 页 PPT，带大家彻底搞懂 Agent Skills。

---

### P2: 目录 (Agenda)
**【PPT内容】**
1. **背景与概念**：为什么需要 Skills？
2. **核心架构**：渐进式披露与三层模型
3. **生态定位**：Skills, MCP, Tools 的关系
4. **开发实战**：最佳实践与真实案例

**【演讲脚本】**
这是今天的议程。我们首先会理清概念，解释为什么传统的 Agent 开发模式遇到了瓶颈。
然后，我们会深入架构内部，看看它是如何通过“渐进式披露”来优化 Token 使用的。
接着，我们会把 Skills 放在整个 AI 生态中，对比它和 MCP、Tools 的区别。
最后，也是最重要的一块，我会通过三个具体的实战案例，展示如何在实际项目中落地 Skills。

---

### P3: Agent 范式的演进
**【PPT内容】**
- **过去：专用 Agent (Specialized Agents)**
  - 独立的 Research Agent, Coding Agent, Marketing Agent
  - 痛点：维护成本高，Scaffolding 重复建设
- **现在：通用 Agent + 技能 (General-purpose Agents + Skills)**
  - 统一的 Runtime (Code Sandbox)
  - 动态加载的 Skills
  - 范式：Code as Universal Interface

**【演讲脚本】**
首先，让我们看看 Agent 开发范式的变化。
在过去，我们倾向于开发“专用 Agent”。如果你需要写代码，你做一个 Coding Agent；需要做市场调研，再做一个 Research Agent。每个 Agent 都有自己独立的 Prompt 和环境，维护起来非常痛苦。
现在，趋势变成了“通用 Agent + 技能”。像 Claude 这样的通用模型，配合一个标准的代码执行环境，本身能力已经很强。我们不需要重新造 Agent，只需要给它“安装”不同的技能包。这就像现在的操作系统，系统是通用的，通过安装不同的 App 来扩展能力。

---

### P4: 什么是 Agent Skills？
**【PPT内容】**
- **定义**：一种扩展 AI 能力的轻量级、开放格式 (Open Standard)
- **本质**：文件夹 = 指令 (Markdown) + 脚本 (Python/Bash) + 资源 (Files)
- **核心特性**：
  - **Portable (可移植)**：跨平台支持 (Claude Code, Claude.ai, SDK)
  - **Composable (可组合)**：Skill A + Skill B = Workflow C

**【演讲脚本】**
那么，什么是 Agent Skill？
从技术上讲，它就是一个**文件夹**。在这个文件夹里，我们按照标准格式放入 Markdown 指令、Python 脚本和参考文件。
它有两个核心特性：
一是**可移植性**。Skills 现在是一个开放标准，你在本地开发的 Skill，可以无缝部署到服务器端，或者分享给社区。
二是**可组合性**。这是它最强大的地方。你可以把“读取 Excel”作为一个 Skill，把“生成 PPT”作为另一个 Skill。当遇到一个复杂任务时，Agent 可以自动组合这两个 Skill 来工作，而不需要你写一个新的大 Prompt。

---

### P5: 为什么需要 Skills？
**【PPT内容】**
- **挑战 1：Context Window 限制**
  - 无法将公司所有文档一次性塞入 Prompt
- **挑战 2：隐性知识 (Implicit Knowledge)**
  - 业务流程往往存在于员工脑子里，而非代码里
- **Skills 的价值**：
  - **On-demand Context**：按需加载上下文
  - **Procedural Knowledge**：固化最佳实践

**【演讲脚本】**
我们为什么非要用 Skills？直接写 Prompt 不行吗？
主要有两个原因。
第一是 **Context Window 的限制**。虽然 LLM 的窗口越来越大，但依然昂贵且有限。如果我们把几百页的 API 文档和几十个业务脚本都塞进 System Prompt，不仅贵，还会严重干扰模型的注意力。
第二是**隐性知识的固化**。很多业务流程（比如“如何通过法律合规审查”）是复杂的、非结构化的。Skills 允许我们将这些流程写成文档和脚本，让 Agent 能够稳定复现这些“隐性知识”。

---

### P6: 核心架构：渐进式披露
**【PPT内容】**
- **Progressive Disclosure (渐进式披露)**
- **设计哲学**：Lazy Loading (懒加载)
- **目标**：
  - Efficiency First (效率优先)
  - Minimize Context Pollution (最小化上下文污染)

**【演讲脚本】**
接下来进入技术深水区。Agent Skills 的核心架构设计理念叫做 **Progressive Disclosure（渐进式披露）**。
做前端或后端的同学对 Lazy Loading（懒加载）一定不陌生。Skills 的设计也是一样的道理：**只有在真正需要的时候，才加载真正需要的内容。**
这种设计最大程度地减少了 Token 的消耗，同时也避免了无关信息对 Agent 的干扰，提高了任务执行的准确率。

---

### P7: 架构详解：三层加载模型
**【PPT内容】**
- **L1: Metadata (元数据)**
  - 启动时加载，常驻内存
  - 极小 (~100 tokens)，用于“索引”
- **L2: Instructions (指令)**
  - 任务匹配时加载
  - `SKILL.md` 正文，告诉 Agent “怎么做”
- **L3: Resources (资源)**
  - 执行时按需加载 (IO 操作)
  - 脚本、大文档、模版 -> **不占 Context** (仅输出进 Context)

**【演讲脚本】**
为了实现懒加载，Skills 架构定义了三层模型：
**Layer 1 是 Metadata**。包括 Skill 的名字和简介。这部分常驻内存，Agent 通过它知道自己“会什么”。
**Layer 2 是 Instructions**。当 Agent 决定使用某个 Skill 时，才会加载它的详细说明书（SKILL.md）。
**Layer 3 是 Resources**。这是最精彩的部分。比如巨大的参考文档或复杂的 Python 脚本，它们作为文件存在磁盘上。Agent 只有在执行到具体步骤时，才会去读取或运行它们。这意味着，你可以拥有一个几百兆的知识库，但在未使用时，它对 Context 的占用是 **零**。

---

### P8: 运行环境：VM 与文件系统
**【PPT内容】**
- **Runtime Environment**
  - Secure Sandbox (安全沙箱)
  - File System Access (读写文件)
- **Capabilities**
  - `cat`, `grep`, `ls` (Bash)
  - `python script.py` (Python)
- **状态持久化**：文件在 Session 期间保留

**【演讲脚本】**
Skills 运行在哪里呢？它们运行在一个安全的 **VM 沙箱**中。
在这个环境里，Agent 拥有标准的文件系统访问权限。它可以读文件、写文件、运行 Python 脚本、执行 Bash 命令。
这非常重要，因为这意味着 Skills 不仅仅是“文本”，它们是**可执行的代码**。Agent 可以利用 Python 强大的生态（pandas, numpy 等）来处理数据，而不是仅靠 LLM 进行不可靠的算术推理。

---

### P9: 生态辨析：Skills vs MCP
**【PPT内容】**
- **MCP (Model Context Protocol)**
  - **角色**：连接器 (Connection)
  - **功能**：提供数据访问 (Access)
  - **例子**：GitHub MCP, Postgres MCP
- **Skills**
  - **角色**：专家 (Expertise)
  - **功能**：提供处理逻辑 (Know-how)
  - **例子**：Code Review Skill, Data Analysis Skill
- **公式**：**MCP (Data) + Skill (Logic) = Value**

**【演讲脚本】**
现在市面上有很多概念，最容易混淆的是 Skills 和 MCP。
简单来说：**MCP 负责“连接”，Skills 负责“思考”。**
MCP Server 就像一根管子，把 Agent 连接到你的数据库或 GitHub 仓库。但是，连接上之后怎么用？怎么查数据？怎么提交代码？这需要 Skills 来指导。
比如，MCP 提供了查询数据库的能力，而“营销分析 Skill”教 Agent 应该写什么样的 SQL 语句来计算 ROI。两者结合，才能发挥最大价值。

---

### P10: 生态辨析：Skills vs Tools & Subagents
**【PPT内容】**
- **vs Tools**
  - Tools 是原子操作 (read_file, run_command)
  - Skills 是**教** Agent 如何组合使用 Tools 的说明书
- **vs Subagents**
  - Subagents 拥有独立的 Context 和 Persona
  - Skills 是可以被 Main Agent 或 Subagent 加载的**知识模块**

**【演讲脚本】**
再对比一下 Tools 和 Subagents。
Tools 是最底层的原子能力，比如“读文件”、“运行命令”。Skills 是构建在 Tools 之上的，它是一份说明书，告诉 Agent 在什么情况下，按什么顺序去调用这些 Tools。
Subagents 则是另一种架构，通常用于极度复杂的任务。有趣的是，Skills 和 Subagents 是兼容的。你可以给你的 Subagent 加载特定的 Skills，让它在某个领域变得更专业。

---

### P11: Skill 的解剖学 (结构规范)
**【PPT内容】**
- **目录结构**
```text
my-skill/
├── SKILL.md           (Required)
├── scripts/           (Optional: Python/Bash)
└── references/        (Optional: Docs)
```
- **YAML Frontmatter (Metadata)**
  - `name`: 唯一标识 (recommend: verb-ing)
  - `description`: 什么时候用？做什么？
- **Markdown Body (Instructions)**
  - Workflow Steps, Examples, Edge Cases

**【演讲脚本】**
好了，如果我们要动手写一个 Skill，它长什么样？
结构非常清晰。核心必须有一个 `SKILL.md` 文件。
文件的头部是 YAML 格式的元数据，定义了名字和描述。注意，描述非常重要，Agent 靠它来判断是否要调用这个 Skill。
正文部分就是标准的 Markdown。你可以在这里写步骤、注意事项、甚至 Few-shot Examples。
如果逻辑复杂，就建立 `scripts` 目录放代码；如果文档太长，就建立 `references` 目录放参考资料。

---

### P12: Context Engineering 最佳实践
**【PPT内容】**
- **500-Line Rule**
  - `SKILL.md` 应保持精简 (<500行)
  - 细节移入 `references/`
- **Degrees of Freedom (自由度控制)**
  - **High Freedom**: 创意任务 -> 仅提供指导原则
  - **Low Freedom**: 合规任务 -> 强制执行脚本
- **Clear I/O**: 明确定义 Input 和 Output 格式

**【演讲脚本】**
写 Skill 的过程，我们称为 **Context Engineering**。这里有几条金科玉律：
第一是 **500行原则**。不要写长篇大论。如果你的说明书超过 500 行，Agent 很容易晕。把细节拆分到 `references` 里的独立文件中。
第二是 **自由度控制**。对于写文案这种任务，给 Agent 高自由度；但对于财务核算，必须限制自由度，强制它调用我们写好的 Python 脚本，保证结果 100% 准确。

---

### P13: 质量保证：测试与评估
**【PPT内容】**
- **Unit Tests for Skills**
  - Input: 特定的 Query + Files
  - Expected Output: 具体的行为或文件结果
- **Example JSON Test Case**:
```json
{
  "skills": ["data-analysis"],
  "queries": ["Analyze sales.csv and generate report"],
  "expected_behavior": ["Generates output.md", "Contains ROI calculation"]
}
```
- **Human Feedback Loop**

**【演讲脚本】**
Skill 写好了，怎么保证它好用？我们需要测试。
我们可以为 Skill 编写单元测试。定义好输入的 Prompt 和测试文件，然后断言 Agent 的输出是否符合预期。比如，是否生成了指定格式的报表？是否调用了特定的脚本？
在正式发布给团队使用前，一定要进行多轮的测试和人工评估。

---

### P14: 现成资源：Pre-Built Skills
**【PPT内容】**
- **Anthropic Skills Repository**
  - 官方维护的通用 Skills 库
- **Key Skills**:
  - `pptx`: 生成 PowerPoint (无需从零写代码)
  - `skill-creator`: 辅助创建新 Skill 的 Meta-Skill
- **策略**: Don't Reinvent the Wheel (不要重复造轮子)

**【演讲脚本】**
在大家动手写之前，有个好消息：你不需要从零开始。
Anthropic 官方提供了一个 Skills 仓库，里面有很多现成的 Skill。
特别推荐两个：
一个是 `pptx` skill，它封装了生成 PPT 的复杂 Python 代码，你直接拿来用就能生成精美的幻灯片。
另一个是 `skill-creator`，这很有意思，它是一个“用来创造 Skill 的 Skill”。你可以告诉 Agent 你想要什么功能，它会帮你生成 Skill 的目录结构和初始文档。

---

### P15: 实战案例 1：市场分析 (Skill + MCP)
**【PPT内容】**
- **场景**：从 BigQuery 获取数据并分析
- **组合**：
  - **BigQuery MCP**: 提供 `query_table` 工具
  - **Marketing Analysis Skill**: 包含 SQL 模版和分析逻辑
- **流程**：
  1. Skill 指导 Agent 生成 SQL
  2. Agent 调用 MCP 执行 SQL
  3. Skill 指导 Agent 用 Python 分析结果

**【演讲脚本】**
接下来看实战案例。第一个是市场分析。
在这个案例中，我们展示了 Skill 和 MCP 的完美配合。
我们要从 BigQuery 查数据。我们安装了 BigQuery MCP Server，它提供了查询能力。
然后我们加载“市场分析 Skill”。这个 Skill 里存了复杂的 SQL 模版。
Agent 运行时，先从 Skill 拿到 SQL 模版，填入参数，然后调用 MCP 去查数据。拿到数据后，再根据 Skill 里的 Python 脚本计算增长率。这就是“大脑”指挥“手脚”的过程。

---

### P16: 实战案例 2：品牌指南 (Brand Guidelines)
**【PPT内容】**
- **场景**：确保所有输出符合公司品牌规范
- **内容**：
  - `assets/logo.png`: 矢量 Logo 文件
  - `references/colors.md`: HEX 色值定义 (#FF5733)
  - `SKILL.md`: 规定字体使用规范
- **应用**：被 PPT Skill 或 Report Skill 引用

**【演讲脚本】**
第二个案例是品牌指南。
每个公司都有品牌规范（Logo、配色、字体）。我们把这些做成一个 `Brand Guidelines Skill`。
在这个 Skill 的 `assets` 目录下放 Logo 图片，在 `references` 下放颜色代码文档。
当其他 Skill（比如 PPT 生成）工作时，Agent 会自动读取这个 Brand Skill 里的颜色配置，确保生成的 PPT 颜色是公司官方配色，而不是随机的。这极大地保证了输出的一致性。

---

### P17: 实战案例 3：完整工作流编排
**【PPT内容】**
- **场景**：每周自动化营销报告
- **Skill Orchestration (技能编排)**：
  - `[BigQuery Skill]` -> 获取原始数据
  - `[Data Analysis Skill]` -> 清洗、计算指标
  - `[Brand Guidelines Skill]` -> 获取配色/Logo
  - `[PPT Generator Skill]` -> 渲染最终报告
- **结果**：一键生成专业级周报

**【演讲脚本】**
最后，我们把所有东西串起来，看一个完整的工作流。
假设我们要生成周报。Agent 会自动进行技能编排：
第一步，调用 BigQuery Skill 抓数据。
第二步，调用分析 Skill 处理数据。
第三步，调用品牌 Skill 拿到 Logo 和配色。
第四步，调用 PPT Skill 将上述所有内容渲染成 PPT。
这就是 Agent Skills 的终极形态——**自动化工作流**。

---

### P18: 总结与行动建议
**【PPT内容】**
- **核心回顾**：
  - **Standardization**: 标准化能力封装
  - **Efficiency**: 渐进式披露节省 Token
  - **Ecosystem**: 结合 MCP 释放潜力
- **Next Steps**:
  1. 浏览 Anthropic Skills Repo
  2. 识别团队中的“重复性工作流”
  3. 尝试编写第一个 Skill (Hello World)

**【演讲脚本】**
总结一下，Agent Skills 不仅仅是一个技术特性，它是 AI Agent 落地的关键基础设施。它让我们可以标准化地封装能力，高效地利用 Token，并结合 MCP 构建强大的应用。
我建议大家会后可以去浏览一下官方的 Skills 库，然后思考一下：咱们团队里有哪些重复性的、繁琐的工作流？试着把它封装成第一个 Skill。
以上就是今天的分享，谢谢大家！

---
