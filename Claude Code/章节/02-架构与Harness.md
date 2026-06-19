# 2. 理解 Claude Code 架构：模型与 Harness

在动手安装之前，先理解 Claude Code 的整体架构，会让你后续使用每一项功能都更加通透。这是本教程最重要的一章。

Claude Code 官方文档中有一个核心术语 —— **Agentic Harness（代理框架）**，并对它下了一个明确的定义：

> **"Claude Code 是 harness（框架）；Claude 是运行在其中的模型。"** Harness 提供文件访问、Shell 执行、权限管控、记忆加载，以及把各个动作串成循环的执行环境。

换句话说，要把一个语言模型变成一个能干活的编程代理，需要两层东西：

- **模型（Model）**：负责"想"——推理、决定下一步调用什么工具、给什么参数。你配置的 GLM-5.2、或 Claude Opus/Sonnet 就是这一层。
- **Harness（框架，即 Claude Code 应用本身）**：负责"做"和"管"——实际执行命令、修改文件、强制权限、加载记忆、把模型的一次次决策串成完整的工作循环。

## 2.1 模型与 Harness 的分工

理解这条边界，是理解 Claude Code 一切行为的关键：

| 维度 | 模型（Claude / GLM）负责 | Harness（Claude Code 应用）负责 |
|------|--------------------------|----------------------------------|
| 推理决策 | 决定调用哪个工具、传什么参数、下一步做什么 | —— |
| 工具执行 | —— | **实际执行** Bash、Edit、Read 等工具并收集结果 |
| 权限 | 只"尝试"调用 | **强制**进行 allow / ask / deny 判定、弹出确认框 |
| 钩子 (Hooks) | 不执行 | 在固定的生命周期点**确定性执行**（而非由模型决定） |
| 记忆 / 上下文 | 只读取已注入的内容 | 加载 CLAUDE.md、自动记忆、压缩对话 (/compact) |
| 技能 (Skills) | 根据描述判断是否触发 | 扫描、发现、热加载技能目录 |
| 子代理 / 任务 | 决定是否委派 | 在隔离上下文中 spawn 子代理并汇总返回 |

当教程里说"Claude 选择"或"Claude 决定"时，指的是**模型**在做推理；而工具真正落地、权限被拦截、钩子被触发，都是 **harness** 在执行。

## 2.2 Harness 管辖的子系统

Claude Code 的 harness 由若干子系统组成，它们也正是本教程后续各章的主题：

1. **权限系统**：决定哪些工具 / 文件 / 域名可以被访问。规则由 harness 强制执行，**不是模型说了算**。详见 [Plan 模式](./06-高级功能与技巧.md#64-使用-plan-模式) 与 [权限问题](./08-故障排除.md#82-权限与认证问题)。
2. **钩子 (Hooks)**：在会话开始、工具调用前后、停止前等固定时机自动运行你的脚本。确定性触发，是自动化与安全审计的核心。详见 [钩子 (Hooks)](./06-高级功能与技巧.md#62-钩子-hooks)。
3. **工具调度**：内置工具（文件、搜索、执行、Web 等）与 MCP 工具、子代理工具，都由 harness 调用并把结果送回模型。
4. **上下文与记忆**：管理对话窗口、自动压缩、加载 CLAUDE.md 和自动记忆。详见 [优化设置（CLAUDE.md）](./07-最佳实践.md#71-优化设置claudemd-文件)。
5. **技能系统**：harness 扫描技能目录，按需注入技能内容。详见 [Claude Skills 使用](./06-高级功能与技巧.md#69-claude-skills-使用)。
6. **子代理与任务**：在隔离上下文中运行子代理，管理任务清单。
7. **会话生命周期**：会话开始 / 恢复 / 结束、非交互模式 (-p) 等。

## 2.3 为什么"由 Harness 执行而非模型"很重要

这是本章最关键、也最容易被忽视的一点：

> **凡是"必须发生"的安全 / 审计行为，应该写进 Hooks 或 managed settings，而不是写进 CLAUDE.md 提示。**

原因：

- **CLAUDE.md 里的指令只是模型"尽量遵循"的建议**。模型可能被提示注入（prompt injection）诱导而违背它。
- **Hooks 与权限规则由 harness 强制执行**，触发时机是固定的生命周期点，"不以模型的意愿为转移"。即便模型被恶意指令诱导，hooks 仍会照常触发。
- 例如：你想"永远禁止删除 `.env` 文件"，正确做法是在权限 `deny` 或 `PreToolUse` hook 中拦截，而不是在 CLAUDE.md 里写一句"不要删除 .env"——后者模型可能不遵守。

掌握这一点，你就能正确区分"软约束（提示）"和"硬约束（harness 强制）"，写出真正可靠的配置。

## 2.4 与 Harness 强相关的 settings.json 字段

绝大多数 harness 行为都可以通过 `settings.json` 调整。常用字段（以官方最新文档为准）：

| 字段 | 作用 |
|------|------|
| `permissions` | 权限规则：`allow` / `ask` / `deny` 数组、`defaultMode`、`additionalDirectories` 等 |
| `hooks` | 钩子配置：按事件 → matcher → handler 组织 |
| `model` | 覆盖默认模型（会话中也可用 `/model` 切换） |
| `env` | 注入环境变量（如 `ANTHROPIC_BASE_URL`、`API_TIMEOUT_MS` 等） |
| `outputStyle` | 输出风格：`Default` / `Proactive` / `Explanatory` / `Learning` 或自定义 |
| `sandbox` | 沙箱：限制 Bash 的文件系统与网络访问 |
| `effortLevel` | 推理强度：`low` / `medium` / `high` / `xhigh`（跨会话持久） |
| `autoCompactEnabled` | 自动压缩开关（默认 `true`） |
| `autoMemoryEnabled` | 自动记忆开关（默认 `true`） |

配置合并优先级（从高到低）：**managed（企业托管）> 命令行参数 > 项目本地 `.claude/settings.local.json` > 项目共享 `.claude/settings.json` > 用户 `~/.claude/settings.json`**。数组类字段（如权限的 allow/deny）跨层合并去重，标量字段遵循覆盖规则。

> **小提示**：你这台机器的配置恰好是"harness = Claude Code 应用、模型 = GLM"的活样本——请求被 harness 通过 `env` 里的 `ANTHROPIC_BASE_URL` 改写到了智谱网关 `open.bigmodel.cn`，并把模型别名映射成了 GLM。理解了架构，再看 [第 3 章的配置](./03-安装与设置.md) 就一目了然了。

---

← [上一章：Claude Code 简介](./01-简介.md) ｜ [返回目录](../README.md) ｜ 下一章 → [安装与设置](./03-安装与设置.md)
