# Claude Code 完整使用教程：从入门到精通

## 目录

1. [Claude Code 简介](#1-claude-code-简介)
2. [理解 Claude Code 架构：模型与 Harness](#2-理解-claude-code-架构模型与-harness)
3. [安装与设置](#3-安装与设置)
   - 3.1 [安装 Claude Code](#31-安装-claude-code)
   - 3.2 [配置 GLM Coding Plan](#32-配置-glm-coding-plan)
   - 3.3 [开始使用 Claude Code](#33-开始使用-claude-code)
   - 3.4 [模型配置说明](#34-模型配置说明)
   - 3.5 [常见问题排查](#35-常见问题排查)
4. [基础使用流程](#4-基础使用流程)
   - 4.1 [启动 Claude Code 会话](#41-启动-claude-code-会话)
   - 4.2 [询问第一个问题](#42-询问第一个问题)
   - 4.3 [首次代码变更](#43-首次代码变更)
   - 4.4 [利用 Git 工作流](#44-利用-git-工作流)
   - 4.5 [调试与新增功能](#45-调试与新增功能)
5. [常见工作流程](#5-常见工作流程)
   - 5.1 [理解新代码库](#51-理解新代码库)
   - 5.2 [高效修复 Bug](#52-高效修复-bug)
   - 5.3 [代码重构](#53-代码重构)
   - 5.4 [编写测试](#54-编写测试)
   - 5.5 [创建 Pull Request](#55-创建-pull-request)
   - 5.6 [处理文档](#56-处理文档)
6. [高级功能与技巧](#6-高级功能与技巧)
   - 6.1 [斜杠命令与自定义命令](#61-斜杠命令与自定义命令)
   - 6.2 [钩子 (Hooks)](#62-钩子-hooks)
   - 6.3 [插件与 MCP](#63-插件与-mcp)
   - 6.4 [使用 Plan 模式](#64-使用-plan-模式)
   - 6.5 [让 Claude 面试你](#65-让-claude-面试你)
   - 6.6 [并行会话与 Git Worktree](#66-并行会话与-git-worktree)
   - 6.7 [作为 Unix 工具使用](#67-作为-unix-工具使用)
   - 6.8 [控制输出格式](#68-控制输出格式)
   - 6.9 [Claude Skills 使用](#69-claude-skills-使用)
   - 6.10 [循环与定时任务 (Loop)](#610-循环与定时任务-loop)
7. [最佳实践](#7-最佳实践)
   - 7.1 [优化设置（CLAUDE.md 文件）](#71-优化设置claudemd-文件)
   - 7.2 [明确具体地提出请求](#72-明确具体地提出请求)
   - 7.3 [分步指导复杂任务](#73-分步指导复杂任务)
   - 7.4 [先让 Claude 探索](#74-先让-claude-探索)
   - 7.5 [使用快捷键](#75-使用快捷键)
   - 7.6 [利用 Plan 模式减少风险](#76-利用-plan-模式减少风险)
   - 7.7 [为敏感数据使用 MCP](#77-为敏感数据使用-mcp)
   - 7.8 [使用 CLI 工具而非 MCP](#78-使用-cli-工具而非-mcp)
   - 7.9 [团队协作标准化](#79-团队协作标准化)
   - 7.10 [持续学习和实验](#710-持续学习和实验)
8. [故障排除](#8-故障排除)
   - 8.1 [安装相关问题](#81-安装相关问题)
   - 8.2 [权限与认证问题](#82-权限与认证问题)
   - 8.3 [配置文件问题](#83-配置文件问题)
   - 8.4 [性能与稳定性问题](#84-性能与稳定性问题)
   - 8.5 [搜索与发现相关问题](#85-搜索与发现相关问题)
   - 8.6 [IDE 集成相关问题](#86-ide-集成相关问题)
   - 8.7 [其他问题](#87-其他问题)
9. [总结](#9-总结)

## 1. Claude Code 简介

**Claude Code** 是 Anthropic 推出的一款智能编程助手，它运行在你的终端中，能够理解你的代码库，并通过自然语言命令来执行日常任务、解释复杂代码、管理 Git 工作流等。Claude Code 的核心优势在于其强大的代码库理解能力和上下文感知能力：它无需你手动上传文件，就能自动读取并分析项目结构，为你的开发任务提供精准的代码建议和自动化支持。与传统的 AI 编程工具不同，Claude Code 并非简单的代码补全引擎，而是一个具备代理（Agentic）能力的编程助手，可以自主决策如何完成任务，并与你进行多轮交互以逐步完善解决方案。

使用 Claude Code，你可以通过自然语言描述来实现从需求到代码的转化。例如，你只需告诉 Claude Code "添加一个用户注册表单"，它就会规划实现方案，编写相应的前端和后端代码，并确保其正常工作。这种能力使 Claude Code 成为开发者的"虚拟编程伙伴"，能够显著提升开发效率，将更多的创意转化为代码。Claude Code 还擅长处理繁琐的开发流程，如自动修复 Lint 错误、解决 Git 合并冲突、生成发布说明等，帮助开发者将更多精力投入到核心逻辑和创意实现上。

Claude Code 设计简洁，遵循 Unix 哲学，具有高度的可组合性和可脚本化特性。这意味着你可以将其灵活地集成到现有的开发工作流中，甚至通过管道（pipe）将其他工具的输出传递给 Claude Code 处理。同时，Claude Code 提供企业级的安全与合规支持，支持通过 Claude API 或在 AWS/GCP 等云平台上运行，满足团队协作和企业部署的需求。Claude Code 在 GitHub 上广受全球开发者关注（具体 Star/Fork 数请以 [官方仓库](https://github.com/anthropics/claude-code) 实时数据为准）。

## 2. 理解 Claude Code 架构：模型与 Harness

在动手安装之前，先理解 Claude Code 的整体架构，会让你后续使用每一项功能都更加通透。这是本教程最重要的一章。

Claude Code 官方文档中有一个核心术语 —— **Agentic Harness（代理框架）**，并对它下了一个明确的定义：

> **"Claude Code 是 harness（框架）；Claude 是运行在其中的模型。"** Harness 提供文件访问、Shell 执行、权限管控、记忆加载，以及把各个动作串成循环的执行环境。

换句话说，要把一个语言模型变成一个能干活的编程代理，需要两层东西：

- **模型（Model）**：负责"想"——推理、决定下一步调用什么工具、给什么参数。你配置的 GLM-5.2、或 Claude Opus/Sonnet 就是这一层。
- **Harness（框架，即 Claude Code 应用本身）**：负责"做"和"管"——实际执行命令、修改文件、强制权限、加载记忆、把模型的一次次决策串成完整的工作循环。

### 2.1 模型与 Harness 的分工

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

### 2.2 Harness 管辖的子系统

Claude Code 的 harness 由若干子系统组成，它们也正是本教程后续各章的主题：

1. **权限系统**：决定哪些工具 / 文件 / 域名可以被访问。规则由 harness 强制执行，**不是模型说了算**。详见 6.4 Plan 模式与 8.2 权限问题。
2. **钩子 (Hooks)**：在会话开始、工具调用前后、停止前等固定时机自动运行你的脚本。确定性触发，是自动化与安全审计的核心。详见 6.2。
3. **工具调度**：内置工具（文件、搜索、执行、Web 等）与 MCP 工具、子代理工具，都由 harness 调用并把结果送回模型。
4. **上下文与记忆**：管理对话窗口、自动压缩、加载 CLAUDE.md 和自动记忆。详见 7.1。
5. **技能系统**：harness 扫描技能目录，按需注入技能内容。详见 6.9。
6. **子代理与任务**：在隔离上下文中运行子代理，管理任务清单。
7. **会话生命周期**：会话开始 / 恢复 / 结束、非交互模式 (-p) 等。

### 2.3 为什么"由 Harness 执行而非模型"很重要

这是本章最关键、也最容易被忽视的一点：

> **凡是"必须发生"的安全 / 审计行为，应该写进 Hooks 或 managed settings，而不是写进 CLAUDE.md 提示。**

原因：

- **CLAUDE.md 里的指令只是模型"尽量遵循"的建议**。模型可能被提示注入（prompt injection）诱导而违背它。
- **Hooks 与权限规则由 harness 强制执行**，触发时机是固定的生命周期点，"不以模型的意愿为转移"。即便模型被恶意指令诱导，hooks 仍会照常触发。
- 例如：你想"永远禁止删除 `.env` 文件"，正确做法是在权限 `deny` 或 `PreToolUse` hook 中拦截，而不是在 CLAUDE.md 里写一句"不要删除 .env"——后者模型可能不遵守。

掌握这一点，你就能正确区分"软约束（提示）"和"硬约束（harness 强制）"，写出真正可靠的配置。

### 2.4 与 Harness 强相关的 settings.json 字段

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

> **小提示**：你这台机器的配置恰好是"harness = Claude Code 应用、模型 = GLM"的活样本——请求被 harness 通过 `env` 里的 `ANTHROPIC_BASE_URL` 改写到了智谱网关 `open.bigmodel.cn`，并把模型别名映射成了 GLM。理解了架构，再看第 3 章的配置就一目了然了。

## 3. 安装与设置

### 3.1 安装 Claude Code

在开始使用 Claude Code 之前，你需要先安装它。Claude Code 支持多种安装方式。

#### 前提条件

- 如果使用 npm 方式：需要安装 Node.js 18 或更新版本环境
- Windows 用户还需安装 Git for Windows
- 原生安装方式（推荐）不依赖 Node.js，安装的是独立二进制

#### 方法一：原生安装（官方推荐）

官方当前**首推原生安装**，不需要 Node.js，也不需要管理员权限：

- **macOS / Linux / WSL**：
```bash
curl -fsSL https://claude.ai/install.sh | bash
```
- **Windows（PowerShell）**：
```powershell
irm https://claude.ai/install.ps1 | iex
```
- 其他可选：`brew install --cask claude-code`（macOS）、`winget install Anthropic.ClaudeCode`（Windows）。

原生安装会部署到 `~/.local/bin`（macOS/Linux）或 `%USERPROFILE%\.local\bin`（Windows），支持后台自动更新。

#### 方法二：npm 安装

使用 npm 全局安装：
```bash
npm install -g @anthropic-ai/claude-code
```
安装完成后查看版本：
```bash
claude --version
```

#### 方法三：Cursor 引导安装

如果你不熟悉 Node.js 且有 Cursor，可以在 Cursor 中输入 `Help me install Claude Code`，Cursor 会引导你完成安装。也可以访问官方文档：[Claude Code 概览](https://code.claude.com/docs/zh-CN/overview)。

#### 注意事项

- 如果在 npm 安装过程中遇到权限问题，MacOS 用户推荐使用 nvm 方式安装 Node.js；必要时可尝试以管理员身份运行。
- 安装成功后，还需进行后续配置步骤（见 3.2），若直接使用 `claude` 命令启动，可能由于网络或地区限制无法使用。

### 3.2 配置 GLM Coding Plan

安装完成后，需要配置 GLM Coding Plan 套餐才能正常使用。配置过程包括注册账号、获取 API Key 和配置环境变量三个步骤。

#### 步骤一：注册账号

访问[智谱开放平台](https://open.bigmodel.cn/)，点击右上角的「注册/登录」按钮，按照提示完成账号注册流程。

#### 步骤二：获取 API Key

- 个人版套餐的用户，通过 **个人编程套餐 > 套餐概览**，新建 API Key。
- 团队版套餐的成员，通过 **团队编程套餐 > 我的套餐** 获取 API Key（团队套餐 Key 与平台其他 API Key 不通用，使用团队额度请务必使用团队套餐 Key）。

请妥善保管你的 API Key，不要泄露给他人，也不要直接硬编码在代码中。

#### 步骤三：配置环境变量

通过设置环境变量来配置 GLM Coding Plan，有以下三种方式可选：

##### 方式一：自动化助手

使用 Coding Tool Helper 快速完成配置：
```bash
npx @z_ai/coding-helper
```
按照界面提示操作即可自动完成工具安装、套餐配置和 MCP 服务器管理等。详细说明请参考 [Coding Tool Helper 文档](https://docs.bigmodel.cn/cn/coding-plan/extension/coding-tool-helper)。

##### 方式二：自动化脚本

仅支持 MacOS 和 Linux 环境（⚠️ 不支持 Windows），在终端或 IDE 中运行以下命令：
```bash
curl -O "https://cdn.bigmodel.cn/install/claude_code_env.sh" && bash ./claude_code_env.sh
```
脚本会自动修改 `~/.claude/settings.json` 来配置环境变量，并在 `~/.claude.json` 添加必要参数。

##### 方式三：手动配置

支持 MacOS、Linux 和 Windows，需手动修改配置文件。

**1. 配置 settings.json**

根据不同系统，编辑或新增对应的 `settings.json` 文件：

- **MacOS & Linux**: `~/.claude/settings.json`
- **Windows**: `用户目录/.claude/settings.json`

添加或修改 `env` 字段：
```json
{
  "env": {
    "ANTHROPIC_AUTH_TOKEN": "your_zhipu_api_key",
    "ANTHROPIC_BASE_URL": "https://open.bigmodel.cn/api/anthropic",
    "API_TIMEOUT_MS": "3000000",
    "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": "1"
  }
}
```
**注意：** 请将 `your_zhipu_api_key` 替换为你在步骤二获取的实际 API Key。

**2. 配置 .claude.json**

编辑或新增 `.claude.json` 文件：

- **MacOS & Linux**: `~/.claude.json`
- **Windows**: `用户目录/.claude.json`

添加以下参数：
```json
{
  "hasCompletedOnboarding": true
}
```
**重要提示：**

- 配置文件需保证 JSON 格式正确性（代码块中的引号必须是英文半角 `"`，不能使用中文全角引号；不能少逗号或多逗号）。
- 配置成功后，请确保重新打开一个新的终端窗口，以便环境配置生效。

### 3.3 开始使用 Claude Code

配置完成后，按照以下步骤开始使用：

1. **进入代码工作目录**：在终端中导航到你的项目目录
2. **启动 Claude Code**：执行以下命令
```bash
claude
```
3. **确认 API Key 使用**：如果遇到「Do you want to use this API Key」的提示，选择 Yes 即可
4. **信任文件访问**：启动后选择信任 Claude Code 访问文件夹里的文件

配置完成！现在就可以正常使用 Claude Code 进行开发了。

### 3.4 模型配置说明

在成功配置套餐后，**默认为服务端模型映射**——即你界面上看到的是 Claude 模型，但实际使用的是 GLM 模型。Claude Code 内部模型环境变量与 GLM 模型的默认对应关系如下：

- `ANTHROPIC_DEFAULT_OPUS_MODEL`：GLM-4.7
- `ANTHROPIC_DEFAULT_SONNET_MODEL`：GLM-4.7
- `ANTHROPIC_DEFAULT_HAIKU_MODEL`：GLM-4.5-Air

一般情况下，使用默认的服务端映射即可，服务端会自动跟进到最新可用模型，无需手动调整。

#### 使用最新的 GLM-5.2 模型（推荐）

GLM 模型迭代很快（GLM-4.5 → 4.6 → 4.7 → GLM-5 → GLM-5.1 → **GLM-5.2**）。如果你想显式使用最新的 **GLM-5.2**（并开启 1M 超长上下文），需要在 `~/.claude/settings.json` 中添加或替换如下环境变量：

```json
{
  "env": {
    "CLAUDE_CODE_AUTO_COMPACT_WINDOW": "1000000",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "glm-5.1",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "glm-5.2[1m]",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "glm-5.2[1m]"
  }
}
```

注意事项：

- **1M 上下文**：模型名后缀加上 `[1m]` 即 `glm-5.2[1m]`，**同时必须**配置压缩窗口大小 `"CLAUDE_CODE_AUTO_COMPACT_WINDOW": "1000000"`。
- **版本要求**：若加了 `[1m]` 后缀后 Claude Code 提示"模型不存在"，请用 `claude update` 升级到最新版本后重试。
- **额度消耗**：GLM-5.2 / GLM-5.1 / GLM-5-Turbo 属于**高阶模型**（对标 Claude Opus），调用时按"高峰期（每日 14:00–18:00 UTC+8）3 倍、非高峰期 2 倍"系数消耗额度；非高峰期有限时 1 倍抵扣福利（以智谱官方公告期限为准）。

#### 切换 effort（思考强度）

在 Claude Code 会话中输入 `/effort` 命令即可切换思考强度。Claude Code 会把所选 effort 映射到 GLM-5.2 实际生效的 effort：

| Claude Code 中选择的 effort | GLM-5.2 实际映射 |
| --- | --- |
| `low`、`medium`、`high`（默认） | `high` |
| `xhigh`、`max`、`ultracode` | `max` |

> 💡 **Coding 任务推荐切换到 `max` effort**，以获取更深度的推理与更稳定的复杂任务表现。

启动新的命令行窗口，运行 `claude` 启动 Claude Code，然后在 Claude Code 中输入 `/status` 即可确认当前模型状态。

### 3.5 常见问题排查

#### 手动修改配置不生效

如果手动修改了 `~/.claude/settings.json` 配置文件但发现配置没有生效，可以尝试以下排查步骤：

1. 关闭所有 Claude Code 窗口，重新打开一个新的命令行窗口，再次运行 `claude` 启动。
2. 如果问题仍然存在，尝试删除 `~/.claude/settings.json` 文件，然后重新配置环境变量。
3. 确认配置文件的 JSON 格式是否正确（引号必须为英文半角、不能少逗号或多逗号），可以使用在线 JSON 校验工具进行检查。

#### 推荐的 Claude Code 版本

建议使用最新版本的 Claude Code，可以通过以下命令检查当前版本和升级：
```bash
# 检查当前版本
claude --version

# 升级到最新版本
claude update
```
官方在 Claude Code 2.1.140 等版本验证可正常工作。

> **注意**：Claude Code **v2.1.69** 版本存在已知 BUG，若使用该版本且需要调用 `claude-opus-4-6`，需额外设置环境变量 `ENABLE_TOOL_SEARCH=0` 和 `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS=1`，否则会异常。建议直接升级到更新版本规避。

#### 配置文件位置说明

- **MacOS & Linux**:
  - 设置文件：`~/.claude/settings.json`
  - 配置文件：`~/.claude.json`
- **Windows**:
  - 设置文件：`用户目录/.claude/settings.json`
  - 配置文件：`用户目录/.claude.json`

通过以上配置步骤，你就完成了 Claude Code 与 GLM Coding Plan 的集成配置，可以开始享受更高效的编程体验了。

## 4. 基础使用流程

在本节中，我们将通过一个简单的示例演示 Claude Code 的基本使用流程，帮助你快速上手。假设你已经按照上一章完成了安装和登录，现在有一个代码项目需要开发或维护。

### 4.1 启动 Claude Code 会话

首先，打开终端并导航到你的项目目录。例如：
```bash
cd /path/to/your/project
```
然后运行 `claude` 命令启动 Claude Code 的交互式会话：
```bash
claude
```
首次运行时，你会看到 Claude Code 的欢迎界面，其中会显示你的会话信息、最近的对话以及最新更新。此时，你可以输入 `/help` 查看所有可用的斜杠命令，或输入 `/resume` 恢复上一次的对话。如果是新安装，`/resume` 可能没有任何内容。

### 4.2 询问第一个问题

现在，让我们从了解你的代码库开始。你可以直接向 Claude Code 提问，例如：
```text
> 这个项目是做什么的？
```
Claude Code 会读取你项目中的文件（如 `README`、主要源代码文件等），然后为你总结这个项目的用途和功能。你也可以提出更具体的问题，例如：
```text
> 这个项目使用了哪些技术？
> 主要的入口文件在哪里？
> 解释一下文件夹的结构
```
Claude Code 都会根据你的代码库内容给出回答。这种能力使得快速上手一个新项目变得非常容易。

此外，你还可以向 Claude Code 询问它自己的能力。例如：
```text
> Claude Code 能做什么？
> 如何使用斜杠命令？
> Claude Code 能和 Docker 一起工作吗？
```
Claude Code 会解释它支持的功能，例如它能执行命令、修改文件、运行 Git 操作等。它还会说明如何使用斜杠命令来执行特定任务，以及它是否支持与你项目中的工具（如 Docker）交互。

### 4.3 首次代码变更

接下来，让 Claude Code 执行一些实际的编码任务。假设你想在项目的**主文件**中添加一个简单的功能，例如一个打印 "Hello, World!" 的函数。你可以直接用自然语言告诉 Claude Code：
```text
> 在主文件中添加一个 hello world 函数
```
Claude Code 会首先定位到项目的主文件（例如 Python 项目中的 `main.py`，Node.js 项目中的 `index.js`），然后显示它计划进行的更改。例如，它可能会展示类似以下的内容：
```diff
+ def hello_world():
+     print("Hello, World!")
```

在 Claude Code 进行实际修改之前，**它总是先征求你的许可**。你可以选择批准这个更改，或者选择"全部批准"模式，让 Claude Code 在当前会话中自动应用后续的所有更改而不必每次确认。这种设计确保了你对代码变更拥有完全的控制权，避免意外的修改。

一旦你批准，Claude Code 就会修改主文件，添加相应的函数代码。你可以继续让它做更多的事情，例如：
```text
> 为主函数添加一个调用 hello_world 的入口
```
Claude Code 会根据你的指示更新代码。通过这种交互方式，你可以像和一个经验丰富的同事对话一样，逐步完成代码的编写和修改。

### 4.4 利用 Git 工作流

Claude Code 对 Git 工作流有原生支持，你可以用自然语言命令它来执行常见的 Git 操作。例如，你可以问：
```text
> 我修改了哪些文件？
```
Claude Code 会列出当前工作目录中被修改的文件列表。接着，你可以让它提交更改：
```text
> 提交我的更改，写一条描述性的提交信息
```
Claude Code 会自动运行 `git add` 添加所有更改，然后撰写一条清晰的提交信息并执行 `git commit`。你也可以让 Claude Code 做更复杂的 Git 操作，例如：
```text
> 创建一个新分支 feature/quickstart
> 显示最近 5 次提交
> 帮我解决合并冲突
```
Claude Code 能够理解这些指令并调用相应的 Git 命令来完成。对于合并冲突等复杂情况，Claude Code 会根据上下文分析冲突内容，并提供解决建议，帮助你顺利完成合并。

### 4.5 调试与新增功能

在日常开发中，你经常会遇到 bug 或需要实现新功能。Claude Code 在这方面同样可以大显身手。你可以用自然语言描述问题或需求，让 Claude Code 来处理。

#### 调试 Bug：

如果你遇到了错误，可以直接把错误信息或错误现象告诉 Claude Code。例如：
```text
> 我在运行单元测试时遇到了一个错误
```
或者
```text
> 修复用户提交表单后出现的一个 bug
```
Claude Code 会根据你的描述定位到相关代码，分析问题原因，并提出修复方案。它可能会修改代码、添加日志，甚至运行测试来验证修复效果。在得到你的许可后，Claude Code 会应用这些更改，从而解决 bug。

#### 实现新功能：

对于新需求，你也可以用自然语言描述。例如：
```text
> 为用户注册表单添加输入验证
```
Claude Code 会理解你的需求，查找相关的前端和后端代码，并实现相应的验证逻辑。它可能需要多轮对话来明确细节，但最终会生成可用的代码。你还可以要求它为这个功能编写单元测试，或更新文档等，让整个流程更加完整。

## 5. 常见工作流程

Claude Code 能够胜任多种常见的开发工作流程。在本节中，我们将介绍一些典型场景，并提供相应的命令示例，帮助你更好地利用 Claude Code 提高效率。

### 5.1 理解新代码库

当你加入一个新项目或接手一个陌生的代码库时，快速理解其结构和功能是非常重要的。Claude Code 能够成为你的"代码导游"，帮助你迅速上手。

#### 获取代码库概览：

你可以直接让 Claude Code 为你提供一个项目概览：
```text
> 给我这个代码库的概览
```
Claude Code 会阅读项目中的主要文件，为你总结项目的架构、主要模块和功能。你可以进一步询问具体细节，例如：
```text
> 这个项目使用了哪些技术栈？
> 解释一下主要的架构模式
> 数据库模型是怎样的？
```
这些对话能帮助你快速建立对项目的整体认知。

#### 定位相关代码：

如果你需要实现或修改某个特定功能，Claude Code 可以帮助你找到相关的代码。例如：
```text
> 找到处理用户认证的文件
```
Claude Code 会列出与认证相关的文件，并解释它们各自的职责。你还可以进一步询问这些文件如何协同工作，例如：
```text
> 这些认证文件是如何一起工作的？
```
这样，你就能理解认证流程在整个系统中的运作方式。

#### 分析执行流程：

当你要调试一个涉及多个组件的问题时，让 Claude Code 追踪执行流程会很有帮助。例如：
```text
> 跟踪从前端到数据库的登录流程
```
Claude Code 会从登录表单提交开始，逐步分析后端的处理逻辑，直到数据库查询，为你展示整个流程。这对于理解复杂系统的运作非常有用。

### 5.2 高效修复 Bug

修复 bug 是开发过程中的家常便饭，Claude Code 可以帮助你更快地定位并修复问题。

#### 共享错误信息：

当你遇到错误时，可以直接把错误消息或堆栈跟踪告诉 Claude Code。例如：
```text
> 我在运行单元测试时遇到了一个错误
```
Claude Code 会分析错误信息，并在代码库中查找可能的原因。你也可以提供复现步骤：
```text
> 提交表单后出现错误，错误信息是 "Invalid input"
```
这些信息能帮助 Claude Code 更准确地定位问题。

#### 获取修复建议：

找到问题后，你可以让 Claude Code 提供修复方案：
```text
> 给出几种修复该 bug 的方法
```
Claude Code 会分析代码上下文，提供一种或多种可行的修复思路。你可以选择其中一种，让 Claude Code 实施修复。

#### 应用修复：

在确认修复方案后，你可以让 Claude Code 直接修改代码：
```text
> 应用你建议的修复
```
Claude Code 会按照你的指示修改相关代码。如果涉及多个文件，它会逐步进行，并在每次修改前征求你的许可。修复完成后，你可以要求 Claude Code 运行测试来验证修复效果：
```text
> 运行测试，确保修复有效
```
通过这种方式，你可以让 Claude Code 自动完成大部分繁琐的调试工作，从而更快地解决问题。

### 5.3 代码重构

随着项目的发展，代码可能需要重构以采用更现代的模式或更清晰的结构。Claude Code 可以帮助你安全地进行重构。

#### 识别遗留代码：

你可以让 Claude Code 帮你找出需要重构的部分。例如：
```text
> 找出代码库中使用已弃用 API 的地方
```
Claude Code 会扫描代码，列出所有使用了已弃用接口的位置。你也可以让它寻找需要优化的模块：
```text
> 找出性能可能较差的代码段
```
这能帮助你确定重构的优先级。

#### 获取重构建议：

对于需要重构的代码，你可以让 Claude Code 提供改进方案：
```text
> 给出重构 utils.js 的建议，使用现代 JavaScript 特性
```
Claude Code 会分析现有代码，并给出一个利用最新语言特性的重构方案。你可以询问这样做的好处，以及是否需要保持向后兼容等。

#### 执行重构：

在确认重构方案后，你可以让 Claude Code 开始重构：
```text
> 开始重构 utils.js
```
Claude Code 会按照建议逐步修改代码。你可以要求它分步进行，并在每一步进行测试，以确保重构过程中不会引入新的 bug：
```text
> 分步进行，每一步都运行测试
```
这种增量式的重构方式能最大限度地降低风险。

#### 验证重构结果：

重构完成后，你可以让 Claude Code 运行完整的测试套件来验证功能是否仍然正常：
```text
> 运行所有测试，确保重构没有破坏任何功能
```
Claude Code 会执行测试，并报告结果。如果有测试失败，它会进一步分析原因并修复，确保重构后的代码既现代化又稳定可靠。

### 5.4 编写测试

编写和维护测试是保证代码质量的重要环节。Claude Code 可以帮助你生成测试代码、运行测试并修复测试失败，从而让测试驱动开发（TDD）变得更容易。

#### 生成测试代码：

你可以让 Claude Code 为某个功能编写单元测试。例如：
```text
> 为计算器函数编写单元测试
```
Claude Code 会分析这些函数的逻辑，并生成相应的测试用例，覆盖正常情况和边界情况。你还可以指定测试框架，例如：
```text
> 使用 pytest 为这个 Python 模块编写单元测试
```
Claude Code 会根据你指定的框架风格来生成测试代码。

#### 运行测试：

编写完测试后，你可以让 Claude Code 运行测试以检查功能是否正常：
```text
> 运行单元测试
```
Claude Code 会调用项目的测试命令（例如 `npm test`、`pytest` 等），并收集测试结果。如果有测试失败，它会进一步分析失败原因，并尝试修复代码。例如：
```text
> 有两个测试失败了，分析原因并修复
```
Claude Code 会查看失败的测试用例，定位到相关代码，并修改代码以使测试通过。这种迭代过程可以大大提高开发效率，减少手动调试的时间。

#### 覆盖率和质量：

Claude Code 还可以帮助你评估测试覆盖率，并改进测试质量。例如：
```text
> 检查测试覆盖率，并为覆盖率低的模块添加更多测试
```
Claude Code 会生成覆盖率报告，并为未充分测试的模块编写额外的测试用例。你还可以要求它进行**安全审计**，例如：
```text
> 对待提交的代码进行安全审计，并修复发现的问题
```
Claude Code 会使用内置的安全检查机制或配置好的子代理，检查代码中的潜在安全问题，并提出修复建议。通过这些手段，Claude Code 能帮助你建立一套完善的测试和质量保障流程。

### 5.5 创建 Pull Request

在团队协作开发中，Pull Request (PR) 是代码审查和合并的重要环节。Claude Code 可以帮助你自动化 PR 的创建过程，并确保 PR 的质量。

#### 创建 PR：

当你完成功能开发并准备好提交时，可以让 Claude Code 为你创建 PR：
```text
> 为当前的更改创建一个 Pull Request
```
Claude Code 会使用 Git 操作创建一个新分支，提交你的更改，并调用 GitHub 的 API 或 CLI 工具来创建 PR。它还会根据你的更改自动生成一个描述性的 PR 标题和正文，以便审阅者了解变更内容。

#### 代码审查：

在创建 PR 之前，你也可以让 Claude Code 对你的更改进行审查：
```text
> 审查我的更改，并提出改进建议
```
Claude Code 会分析你修改的代码，检查代码风格、潜在 bug 和性能问题等，并给出改进意见。你可以根据这些建议进一步完善代码，然后再提交 PR。

#### 处理 PR 评论：

如果 PR 提交后审阅者提出了评论或修改建议，Claude Code 也可以帮助你处理。例如：
```text
> 查看最近一个 PR 的评论
```
Claude Code 会显示 PR 上的评论列表。你可以让 Claude Code 针对某条评论进行修改：
```text
> 修复评论 #123 中提到的问题
```
Claude Code 会根据评论内容修改代码，并提交新的 commit。你还可以让 Claude Code 帮助回复评论或补充说明，从而加速 PR 的流程。

#### 自动化流程：

通过结合 **Hooks** 和 **CI/CD**，你可以让 PR 的创建和检查更加自动化。例如，可以配置一个 Hook 在每次提交后自动运行测试和代码检查，并将结果附加到 PR 上。Claude Code 也可以集成到 CI 中，作为代码审查的一部分。这些高级用法将在后续章节介绍。

### 5.6 处理文档

文档是项目的重要组成部分，但编写和维护文档往往被忽视。Claude Code 可以帮助你自动生成和更新文档，确保文档与代码同步。

#### 生成 README：

如果你刚完成一个新功能或重构了某个模块，可以让 Claude Code 更新 README 文档：
```text
> 更新 README，添加关于新功能的使用说明
```
Claude Code 会阅读代码中的注释和功能描述，然后生成相应的 README 内容。你还可以指定格式或语言，例如：
```text
> 用 Markdown 格式更新 README，并包括代码示例
```
Claude Code 会按照你的指示编写文档。

#### 生成 API 文档：

对于 API 项目，你可以让 Claude Code 生成接口文档：
```text
> 为这个 API 生成文档，包括每个端点的参数和返回值说明
```
Claude Code 会分析代码中的路由定义、参数校验和返回数据结构，自动生成清晰的 API 文档。

#### 代码注释和 JSDoc：

Claude Code 也可以帮助你在代码中添加注释或 JSDoc，以提高代码的可读性。例如：
```text
> 为这个 JavaScript 模块添加 JSDoc 注释
```
Claude Code 会为函数、类等添加类型和功能说明注释。你还可以要求它生成**内联注释**来解释复杂逻辑：
```text
> 在这个复杂的算法代码中添加注释，解释每一步的作用
```
通过这些方式，Claude Code 可以让你的项目文档更加完善和准确，减少手动编写文档的工作量。

## 6. 高级功能与技巧

Claude Code 提供了许多高级功能和配置选项，让你能够将其打造成一个完全符合个人和团队需求的编程助手。在本节中，我们将介绍一些进阶用法和技巧，帮助你充分发挥 Claude Code 的潜力。

### 6.1 斜杠命令与自定义命令

Claude Code 的交互式界面支持**斜杠命令（slash commands）**，这是一种通过命令前缀来快速执行特定任务的机制。斜杠命令在许多方面类似于你可能在其他应用中见到的命令（例如 Slack 的 /command 或 Discord 的 /命令），但 Claude Code 的斜杠命令更为强大，因为它们可以接受参数并与你的代码库深度集成。

#### 内置斜杠命令：

Claude Code 自带了许多内置的斜杠命令，用于常见的操作和配置。以下是一些常用的内置斜杠命令及其作用：

- `/help`：显示所有可用命令的列表和简要说明。
- `/clear`（别名 `/reset`、`/new`）：清除当前的对话历史，相当于重新开始一次对话。
- `/exit`（别名 `/quit`）：退出 Claude Code 的交互式会话。
- `/plan`：打开 Plan 模式。
- `/resume`（别名 `/continue`）：查看历史对话情况。
- `/config`（别名 `/settings`）：打开 Claude Code 的设置界面，你可以在此修改各种配置选项。
- `/agents`：管理和查看自定义的子代理（Agents）列表，也可以创建新的子代理。
- `/permissions`：查看或修改当前的权限策略，例如添加允许不经确认直接执行的命令。
- `/bug`：报告一个 bug（`/feedback` 的别名），它会将当前的对话内容发送给支持团队。
- `/init`：初始化项目，它会为你生成一个 `CLAUDE.md` 文件，用于指导 Claude Code 理解你的项目。
- `/mcp`：管理 Model Context Protocol (MCP) 服务器的连接和认证。
- `/plugin`：管理 Claude Code 的插件，例如启用、禁用或安装插件。
- `/status`：显示当前会话的状态信息，包括模型版本、账户信息、网络连接状态等。
- `/usage`（别名 `/cost`、`/stats`）：显示你的使用统计信息。
- `/effort`：切换思考强度（详见 3.4）。

这些内置命令涵盖了从基础会话管理到高级配置的各个方面，你可以通过 `/help` 查看完整列表。

#### 自定义斜杠命令：

除了内置命令，Claude Code 还允许你创建**自定义斜杠命令**，以便将常用的提示或任务流程封装成命令。自定义命令实际上是存储在 Markdown 文件中的提示模板，当你在对话中调用该命令时，Claude Code 会读取文件内容并执行其中的提示。

自定义命令分为**项目命令**和**个人命令**两种作用域。

- **项目命令：**存储在项目的 `.claude/commands/` 目录下。项目命令会与代码仓库一起提交，供团队中的所有人使用。例如，你可以创建一个 `.claude/commands/deploy.md` 文件，其中包含部署流程的提示，这样团队中的每位成员都可以通过 `/deploy` 命令来运行部署流程。
- **个人命令：**存储在用户目录下的 `~/.claude/commands/` 目录中。个人命令仅对当前用户可用，适用于你个人常用的命令或脚本。例如，你可以创建一个 `~/.claude/commands/review-pr.md`，其中包含代码审查的提示，这样你可以在任何项目中使用 `/review-pr` 来审查代码。

自定义命令的**命名**与其文件名相关：命令名就是文件名去掉 `.md` 后缀。例如，`deploy.md` 对应的命令名就是 `/deploy`。如果项目命令和个人命令同名，则项目命令优先，个人命令会被忽略。

自定义命令的**参数**支持使用占位符来动态传入内容。主要有以下两种方式：

- **`$ARGUMENTS` 占位符：**捕获命令调用时传入的所有参数。例如，在命令文件中写有 `Fix issue #$ARGUMENTS`，当你在对话中输入 `/fix-issue 123 high-priority` 时，`$ARGUMENTS` 将被替换为 "123 high-priority"。
- **`$1`, `$2` 等位置参数：**允许你分别访问传入的第 1 个、第 2 个等参数。例如，命令文件中有 `Review PR #$1 with priority $2`，当你输入 `/review-pr 456 high` 时，`$1` 为 "456"，`$2` 为 "high"。位置参数适合需要单独处理每个参数的场景。

自定义命令的**语法**非常简单，你只需要在 Markdown 文件中撰写提示即可。Claude Code 会将文件内容作为提示发送给模型执行。例如，一个简单的自定义命令 `.claude/commands/optimize.md` 内容如下：
```markdown
分析这段代码的性能问题，并给出优化建议。
```
那么在对话中输入 `/optimize` 时，Claude Code 就会执行这个提示，分析当前代码并给出性能优化建议。

#### 命令示例：

下面我们通过几个示例来展示自定义斜杠命令的用途：

- **代码审查命令：**创建一个 `.claude/commands/review.md`，内容为：
```markdown
审查这段代码的安全性，并提出改进建议。
```
  这样你可以通过 `/review` 快速启动代码安全审查流程。

- **部署命令：**创建一个 `.claude/commands/deploy.md`，内容为：
```markdown
按照以下步骤部署这个项目：
1. 运行构建命令
2. 运行测试
3. 如果测试通过，将代码部署到生产环境
```
  这样你可以通过 `/deploy` 来执行部署流程，Claude Code 会按照提示逐步执行构建、测试和部署等命令。

- **带参数的命令：**创建一个 `.claude/commands/fix-issue.md`，内容为：
```markdown
修复 issue #$ARGUMENTS 中描述的问题。
```
  然后你可以通过 `/fix-issue ENG-123` 来启动修复该 issue 的流程，Claude Code 会使用你的描述和 issue 详情来实施修复。

通过自定义斜杠命令，你可以将常用的开发任务自动化，提高工作效率。命令的创建和使用都十分灵活，你可以根据团队和个人的需求自由定制。

### 6.2 钩子 (Hooks)

**钩子（Hooks）**是 Claude Code 提供的一种强大的扩展机制，由 **harness（框架）而非模型**在特定生命周期事件发生时自动执行你的脚本。这一点至关重要：钩子是**确定性触发**的——在固定的生命周期点运行，不以模型的意愿为转移，因此即使模型被提示注入诱导，钩子仍会照常执行。这使得钩子成为实现自动化流程与安全审计的可靠手段。

#### 配置位置

钩子配置在 **`settings.json` 的 `hooks` 字段**中（不是独立的 `hooks.json` 文件）：

- 用户级（所有项目生效）：`~/.claude/settings.json`
- 项目级（随仓库共享）：`.claude/settings.json`
- 本地项目级（不提交）：`.claude/settings.local.json`

#### 配置结构

钩子采用**三层嵌套**结构：`事件名 → matcher 组数组 → hooks（handler）数组`。每个 handler 至少有 `type` 和 `command` 字段：

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "echo '即将执行 Bash 命令'"
          }
        ]
      }
    ],
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "npm run lint"
          }
        ]
      }
    ]
  }
}
```

- `matcher`：匹配工具名（如 `Bash`、`Edit|Write`），或某些事件的子类型（如 `SessionStart` 的 `startup`/`resume`/`clear`/`compact`）。
- `type`：handler 类型，支持 `command`（运行命令）、`http`、`mcp_tool`、`prompt`、`agent`。最常用的是 `command`。

#### 常用事件类型

Claude Code 提供了丰富的钩子事件，主要包括（注意事件名大小写）：

| 类别 | 事件名 |
|------|--------|
| 会话生命周期 | `SessionStart`、`SessionEnd` |
| 每轮提示 | `UserPromptSubmit`、`Stop`、`SubagentStop` |
| 工具调用 | `PreToolUse`、`PostToolUse` |
| 压缩 | `PreCompact` |
| 通知 | `Notification` |

> ⚠️ 注意：事件名是 `SessionStart` / `SessionEnd`，**不是** `OnSessionStart` / `OnSessionEnd`。

#### 钩子能做什么

钩子不仅可以"执行命令"，还能**拦截和阻止**行为，这是它最强大的能力：

- **`PreToolUse`**：在工具执行前运行，可返回决策 `allow` / `ask` / `deny` 来放行、询问或**阻止**该工具调用。
- **`UserPromptSubmit`**：可 `block` 并擦除用户的某次输入。
- **`Stop` / `SubagentStop`**：可阻止 Claude 提前停下来，让它继续工作。

钩子命令的退出码语义：

- **exit 0**：放行，无特殊决策。
- **exit 2**：阻断错误（blocking error），stderr 内容会反馈给 Claude 让其调整。
- **其他非零**：非阻断错误（non-blocking error），记录但继续。

#### 实用示例

**1. 编辑文件后自动运行测试 / 格式化：**
```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          { "type": "command", "command": "npm test" }
        ]
      }
    ]
  }
}
```

**2. 拦截危险命令（禁止 `rm -rf`）：**
```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "${CLAUDE_PROJECT_DIR}/.claude/hooks/block-rm.sh"
          }
        ]
      }
    ]
  }
}
```
其中 `block-rm.sh` 检查命令内容，若匹配 `rm -rf` 则 `exit 2` 并输出拒绝原因。

**3. 记录所有 Bash 命令到日志（审计）：**
```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          { "type": "command", "command": "echo \"[$(date)] 执行 Bash 命令\" >> ${CLAUDE_PROJECT_DIR}/claude.log" }
        ]
      }
    ]
  }
}
```

**4. 会话开始时加载环境：**
```json
{
  "hooks": {
    "SessionStart": [
      {
        "matcher": "startup",
        "hooks": [
          { "type": "command", "command": "echo '会话开始，环境就绪'" }
        ]
      }
    ]
  }
}
```

#### 安全提示

`command` 类型的钩子**以你系统用户的完整权限运行**，因此：

- 添加钩子前务必审查和测试钩子脚本。
- 正如第 2 章所述：凡是"必须发生"的安全 / 审计行为，应放进钩子或权限规则（harness 强制执行），而不是写进 CLAUDE.md 提示（模型只会"尽量"遵守）。

通过钩子，你可以让 Claude Code 成为一个高度自动化、高度定制的开发助手。它不仅能执行命令，还能在合适的时候介入你的工作流程，为你节省时间和精力。

### 6.3 插件与 MCP

Claude Code 的**插件系统**和**Model Context Protocol (MCP)** 集成极大地扩展了其能力，使其能够连接到外部工具和服务，执行更复杂的任务。

#### 插件系统：

Claude Code 的插件允许你为其添加**自定义命令**、**子代理**和**工作流**，从而满足特定需求。插件本质上是一些包含配置和脚本的目录，可以由你或社区创建。安装插件后，Claude Code 会将其集成到交互界面中，就像内置功能一样使用。

- **发现和安装插件：**你可以从 GitHub 等社区获取别人分享的插件，也可以自行创建。官方提供了一个插件市场，你可以通过 `/plugin` 命令来浏览和安装预置的插件。
- **插件功能：**一个插件可以提供以下几类功能：
  - **自定义斜杠命令：**插件可以定义新的斜杠命令，扩展 Claude Code 的命令集。
  - **子代理：**插件可以创建专门的子代理，用于特定领域的任务。
  - **钩子脚本：**插件可以包含钩子脚本，在特定事件发生时执行插件逻辑。
  - **MCP 服务器：**插件可以捆绑 MCP 服务器，当插件启用时自动提供外部工具集成（详见下文 MCP 部分）。
- **插件管理：**通过 `/plugin` 命令，你可以列出所有已安装的插件、启用或禁用某个插件，以及查看插件的详细信息。

#### MCP (Model Context Protocol)：

MCP 是一种开源标准，用于将 AI 工具（如 Claude Code）与外部服务和数据源连接起来。Claude Code 既可以用作 MCP 客户端，也可以作为 MCP 服务器，这使得它能够与数百种工具和服务集成。

- **Claude Code 作为 MCP 客户端：**当 Claude Code 作为 MCP 客户端时，它可以连接到各种 MCP 服务器，使用这些服务器提供的工具。MCP 服务器可以封装任何外部服务，例如数据库、API、图形设计工具等。
  - **添加 MCP 服务器：**使用 `claude mcp add` 命令来添加一个 MCP 服务器连接。语法为：
```bash
claude mcp add [选项] <名称> -- <命令> [参数...]
```
其中 `--`（ASCII 双连字符）用于分隔 Claude 的选项和服务器命令。`<名称>` 是你给这个服务器起的标识符。

  - **传输类型：**MCP 支持四种传输方式：
    - **HTTP**（`--transport http`）：推荐，适用于云服务。
    - **stdio**（`--transport stdio`）：本地进程，适用于本地脚本 / 工具。
    - **SSE**（`--transport sse`）：**已弃用（deprecated）**，建议改用 HTTP。
    - **WebSocket**：通过 `.mcp.json` 或 `claude mcp add-json` 配置。

  - **环境变量：**有些 MCP 服务器需要环境变量或认证令牌，用 `--env KEY=VALUE` 传递。注意 `--env` 与服务器名之间应插入其他选项（如 `--transport stdio`），否则解析可能出错：
```bash
claude mcp add --env API_KEY=xyz --transport stdio my-server -- python /path/to/server.py
```
这会启动一个 Python MCP 服务器，并传递 `API_KEY` 环境变量。

  - **管理 MCP 服务器：**`claude mcp list` 查看所有已配置的服务器，`claude mcp get <名称>` 查看详情，`claude mcp remove <名称>` 移除。在交互式会话中也可运行 `/mcp` 检查状态。

- **Claude Code 作为 MCP 服务器：**Claude Code 本身也可以作为一个 MCP 服务器，供其他应用（如 IDE、自定义脚本）通过 MCP 协议调用其能力。

- **MCP 示例：**
  - **连接 Jira：**添加一个 Jira MCP 服务器，然后在 Claude Code 中说："为 Jira issue ENG-4521 创建一个 PR"。Claude Code 会通过 MCP 从 Jira 获取 issue 详情，然后实现功能并创建 PR。
  - **数据库查询：**连接 PostgreSQL MCP 服务器，让 Claude Code 查询数据库："查找使用了 ENG-4521 功能的 10 位用户的邮箱"。
  - **设计集成：**连接 Figma、Google Drive 等 MCP 服务器，让 Claude Code 访问设计稿和文档。

#### MCP 配置范围：

MCP 服务器配置支持作用域概念，可以在项目、用户或托管级别配置。例如，你可以在项目根目录添加一个 `.mcp.json` 文件，其中定义了项目需要的 MCP 服务器，这样团队的每个人都会自动拥有这些服务器连接。

通过插件和 MCP，Claude Code 能够成为一个开放的平台，连接到你工作中的各种工具和服务。

### 6.4 使用 Plan 模式

**Plan 模式**是 Claude Code 提供的一种特殊权限模式（官方名 `plan`），它将 Claude Code 限制为只读操作，不会修改任何文件。这种模式非常适合用于代码审查、方案规划或在需要谨慎操作的场景下深入了解代码库。

Plan 模式的主要用途包括：

- **多步骤实现规划：**当你需要实现一个涉及多个文件和步骤的功能时，先使用 Plan 模式规划整体方案，可以避免遗漏和混乱。
- **代码探索：**当你希望深入分析代码库的某一部分，但暂时不想做任何修改时，Plan 模式能让你安全地提问和浏览。
- **交互式开发：**当你希望与 Claude Code 共同讨论实现方案、逐步明确需求时，Plan 模式可以避免过早地修改代码。

#### 权限模式

Claude Code 共有几种权限模式，可通过 `Shift+Tab` 循环切换（顺序：`default` → `acceptEdits` → `plan`）：

| 模式 | 说明 |
|------|------|
| `default` | 默认模式，每次写操作前都询问 |
| `acceptEdits` | 自动批准文件编辑及常用文件系统命令 |
| `plan` | 只读分析，只出方案不改代码 |
| `auto` | 经分类器后台安全检查后全自动（需账户满足条件） |
| `bypassPermissions` | 跳过所有权限检查（仅限隔离容器 / VM） |

#### 切换与启动

在交互式会话中按 `Shift+Tab` 循环切换模式。也可以在启动时指定：
```bash
claude --permission-mode plan
```
或以 Plan 模式执行一次性查询：
```bash
claude -p --permission-mode plan "分析认证系统并提出改进建议"
```
这样会以 Plan 模式运行该查询，然后退出，不会修改任何文件。

在 Plan 模式下，Claude Code 会采用 `AskUserQuestion` 工具来与你交互，以便在规划过程中收集更多信息。例如，在规划认证迁移时，它可能问你："是否需要保持向后兼容？"等。

Plan 模式还可以通过配置设为默认模式，在 `settings.json` 中设置：
```json
{
  "permissions": {
    "defaultMode": "plan"
  }
}
```
这样新会话都会以 Plan 模式开始。

### 6.5 让 Claude 面试你

Claude Code 提供了一种独特的交互方式：**让 Claude 主动提问，你来回答**。这种方式被称为"让 Claude 面试你"或"需求收集"模式。在某些情况下，这种反向的交互比直接让 Claude 开始编码更有效，尤其是在需求尚未明确的时候。

你可以通过在对话中明确指示来启动这种模式。例如：
```text
> 在开始编码之前，请先向我提问，以明确这个功能的需求：用户通知系统
```
Claude Code 会进入"面试"模式，向你提出一系列问题来澄清功能需求。例如：
```text
> 这个通知系统需要支持哪些通知渠道（例如邮件、短信、站内消息）？
> 用户是否可以订阅不同类型的通知？
> 通知的内容是固定的还是可以自定义？
```
通过这些问题，Claude Code 能够更全面地了解你的需求。当收集到足够信息后，它会总结出一个需求规格说明书，并据此开始编码。由于在编码前已经明确了大部分细节，因此生成的代码往往更符合预期，减少了返工的可能。

这种"面试"模式在 Plan 模式下尤为常见。你也可以通过在项目的 `CLAUDE.md` 文件中添加指导来鼓励 Claude Code 主动提问：
```markdown
始终在有多种可行方案时主动提出澄清问题。
```
让 Claude 面试你的方式适用于复杂功能、大型项目的开发，以及团队协作中需求讨论等场景。

### 6.6 并行会话与 Git Worktree

Claude Code 支持同时运行多个会话，并且可以结合 Git Worktree 实现并行开发。

#### 并行会话：

你可以在不同的终端窗口中分别启动 Claude Code，同时进行多个对话。每个会话都是独立的，拥有自己的上下文和状态。例如，一个会话用于编写新功能，另一个会话用于调试，互不干扰。

#### Git Worktree 集成：

Git Worktree 允许你在同一个仓库中同时检出多个分支，每个分支都在不同的目录中工作。例如：
```bash
git worktree add ../feature-a feature-a
git worktree add ../bugfix-b bugfix-b
```
这样你就有了 `../feature-a` 和 `../bugfix-b` 两个工作目录。你可以在各自目录下启动独立的 Claude Code 会话，互不干扰。

#### 注意事项：

- 确保每个会话运行在不同的工作目录下，以避免上下文混淆。
- 如果多个会话访问同一个文件或资源，可能需要协调操作以避免冲突。
- 并行会话会消耗更多资源（如内存和 API 调用），请合理使用。

### 6.7 作为 Unix 工具使用

Claude Code 的设计遵循 Unix 哲学，这使得它能够像其他命令行工具一样组合使用。

#### 管道输入：

```bash
cat app.log | claude -p "如果在日志中看到任何异常，请通知我"
```
使用 `-p`（即 `--print`）选项表示**非交互模式**：Claude Code 会在处理完输入后直接退出，不会进入交互式 REPL。注意 `-p` 仍然是完整的 Agent 循环（可调用工具、读文件），只是不进入交互界面。

#### 重定向输出：

```bash
claude -p "解释一下这个函数的作用" > explanation.txt
```

#### 结合其他工具：

- **日志分析**：将应用日志通过管道传给 Claude Code，让它在发现问题时通知你。
- **代码生成**：将设计文档通过管道传给 Claude Code，让它生成代码框架。
- **测试报告**：将测试输出传给 Claude Code，让它分析失败原因。
- **翻译任务**：
```bash
echo "Hello, World!" | claude -p "将这段文本翻译成法语"
```

#### 作为 CI 任务：

```bash
claude -p "如果发现新的文本字符串，将其翻译成法语并创建一个 PR"
```

通过将 Claude Code 作为 Unix 工具使用，你可以将其融入几乎任何工作流程。

### 6.8 控制输出格式

默认情况下，Claude Code 会以易读的自然语言格式输出结果。但在某些场景下，你可能需要更结构化或特定格式的输出。

#### 输出风格（output style）：

Claude Code 支持多种输出风格，如 `Default`、`Proactive`、`Explanatory`、`Learning` 等。要切换输出风格，请使用 **`/config`（或 `/settings`）命令**，在设置界面中选择 Output style（不存在独立的 `/output-style` 命令）。也可以在 `settings.json` 中设置 `"outputStyle": "explanatory"` 全局指定。

#### 代码块格式化：

当 Claude Code 生成代码时，它会自动将代码包裹在 Markdown 代码块中，并根据语言类型添加适当的语言标签（如 `python`、`javascript`），以便在支持语法高亮的编辑器中正确显示。

#### JSON 输出：

对于脚本或自动化工具，你可以让 Claude Code 以 JSON 格式输出，以便程序解析。使用 `--output-format` 选项，支持 `text`（默认）、`json`、`stream-json` 三个值：
```bash
claude -p "列出所有文件的行数" --output-format json
```
这会输出一个结构化 JSON 对象（含结果、会话 ID、token 消耗等），非常适合与 CI/CD 工具集成。

#### 自定义提示词：

你还可以通过提示词来控制输出的格式和风格。例如，要求 Claude Code "以表格形式列出所有接口"，它就会使用 Markdown 表格输出。

通过合理地控制输出格式，你可以让 Claude Code 的输出更好地适应你的下游工具和需求。

### 6.9 Claude Skills 使用

参考文档 [Claude skills.md](../Claude%20Skills/Claude%20skills.md)。

### 6.10 循环与定时任务 (Loop)

Claude Code 可以让一个任务**周期性或定时地自动运行**，这对于轮询 CI、照看 PR、定时检查部署等场景非常有用。Claude Code 提供了**三种独立的调度方案**，理解它们的区别是正确使用的前提。

> **版本要求**：本节功能需要 Claude Code **v2.1.72 或更高版本**（用 `claude --version` 检查）。

#### 三种调度方案对照

| 维度 | Cloud Routines | Desktop 定时任务 | `/loop` |
|------|----------------|------------------|---------|
| 运行位置 | Anthropic 云端 | 你的本机 | 你的本机 |
| 需要机器开机 | 否 | 是 | 是 |
| 需要会话保持打开 | 否 | 否 | **是** |
| 跨重启持久化 | 是 | 是 | 仅 `--resume` / `--continue` 时恢复未过期任务 |
| 访问本地文件 | 否（全新 clone） | 是 | 是（继承会话） |
| 最小间隔 | 1 小时 | 1 分钟 | 1 分钟 |

本节重点介绍最常用的 **`/loop`**。

#### `/loop` 是什么

`/loop` 是一个 **bundled skill（内置技能）**，而不是普通的斜杠命令。它是在会话保持打开期间，让一个 prompt 周期性重复运行的最快方式。

`/loop` 有三种用法，由你提供的内容决定行为：

| 你提供什么 | 示例 | 行为 |
|------------|------|------|
| 间隔 + prompt | `/loop 5m check the deploy` | **固定间隔** cron |
| 仅 prompt | `/loop check the deploy` | **动态自适应**间隔 |
| 仅间隔 / 空 | `/loop` 或 `/loop 15m` | 运行内置维护 prompt（照看当前分支 PR） |

间隔单位支持 `s`（秒）、`m`（分）、`h`（时）、`d`（天），**最小间隔为 1 分钟**（cron 只有分钟粒度，秒会被向上取整）。也可以把另一个斜杠命令 / 技能当 prompt 传入，例如 `/loop 20m /review-pr 1234`。

#### 两种模式

**1. 固定间隔模式**（`/loop 5m /foo`）

底层用 `CronCreate` 创建固定 cron，按固定节奏运行。适合固定时段同步、定时提醒、固定节奏健康检查。

**2. 动态自适应模式**（`/loop /foo`，不给间隔）

底层用 `ScheduleWakeup` 工具，由 Claude 在每轮迭代结束时**自己决定**下一次何时唤醒（在 1 分钟～1 小时之间自适应）。适合轮询会变化的任务（CI 构建、PR 评审）——任务忙就勤看，闲了就少看。当 Claude 判定任务真正完成时，会自动不再安排下次唤醒（自停）。

> ⚠️ **勘误**：所谓"动态模式默认 10 分钟"是误解。在 Anthropic 直连下，动态模式是 1 分钟～1 小时自适应；只有在 **Bedrock / Vertex AI / Microsoft Foundry** 等不支持 `ScheduleWakeup` 的平台上，才会退化为固定 10 分钟。

#### cron 表达式参考

固定间隔和一次性任务都使用标准 5 段 cron：`分 时 日 月 周`，按**本地时区**解释：

| 示例 | 含义 |
|------|------|
| `*/5 * * * *` | 每 5 分钟 |
| `0 * * * *` | 每小时整点 |
| `0 9 * * *` | 每天本地早上 9 点 |
| `0 9 * * 1-5` | 工作日早上 9 点 |
| `30 14 15 3 *` | 3 月 15 日下午 2:30 |

#### 自定义 loop prompt（loop.md）

如果只运行 `/loop`（不带 prompt），默认会运行内置维护 prompt（继续未完成工作、照看当前分支 PR、空闲时做清理）。你也可以用自定义文件替换它（取第一个找到的）：

- `.claude/loop.md`（项目级，优先）
- `~/.claude/loop.md`（用户级）

纯 Markdown，无强制结构，超过 25000 字节会截断。示例：
```markdown
Check the `release/next` PR. If CI is red, pull the failing job log,
diagnose, and push a minimal fix. If everything is green and quiet,
say so in one line.
```

#### 典型用例

```text
/loop 5m check if the deployment finished and tell me what happened
```
```text
/loop check whether CI passed and address any review comments
```
```text
/loop 20m /review-pr 1234
```

一次性提醒也可以用自然语言（Claude 会换算成 cron 并确认触发时间，跑完自动删除）：
```text
remind me at 3pm to push the release branch
in 45 minutes, check whether the integration tests passed
```

#### 停止与查看

- 按 **`Esc`**：清除当前等待中的 `/loop` 唤醒（只对当前 `/loop` 生效）。
- 动态模式：Claude 判定任务完成时会**自停**。
- 固定模式：跑到按 Esc 或 **7 天自动过期**为止。
- 询问"我现在有哪些定时任务？"可列出；"取消 deploy 检查任务"可删除。

#### 注意事项与坑

1. **仅 REPL 空闲时触发**：定时任务在你两次对话之间触发，Claude 正忙时会等到当前 turn 结束。**没有补跑（catch-up）**——错过的间隔不会补，最多空闲时触发一次。
2. **7 天自动过期**：周期性任务在创建 7 天后自动跑最后一次并删除自己。需要更长寿命请用 Routines 或 Desktop 定时任务。
3. **时区是本地时区**，不是 UTC。
4. **避开整点**：cron 分钟建议不要落在 `:00` / `:30`，否则一次性任务可能提前最多 90 秒、周期任务可能延后最多 30 分钟触发（jitter）。用 `7 * * * *` 而不是 `0 * * * *` 可以避开。
5. **完全禁用调度**：设置环境变量 `CLAUDE_CODE_DISABLE_CRON=1` 可关闭整个调度系统。

#### 🎯 针对本机 GLM 环境的特别说明

- 你当前通过**智谱 GLM 网关**（非 Anthropic 直连）使用 Claude Code。`/loop` 的 cron / 调度工具链在本环境下可用（固定间隔模式无虞）。
- 但动态模式背后的更优路径 **Monitor 工具**（v2.1.98+，比轮询更省 token、更及时）**会因你的 `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1` 设置而被禁用**。这意味着动态 `/loop` 在你这台机器上会真正按轮询跑，无法退化到高效的 Monitor 路径。若要体验 Monitor 的高效形态，需临时去掉该环境变量。
- 第三方 Anthropic 兼容网关（如智谱）下，`ScheduleWakeup` / `Monitor` 等工具的可用性官方文档未明确保证，**建议实测**。

#### 延伸：`/loop` vs `/goal` vs Stop hook

| 方案 | 下一次 turn 何时开始 | 何时停止 |
|------|----------------------|----------|
| `/loop` | 时间间隔到达时 | 你停止它，或 Claude 判定工作完成 |
| `/goal` | 上一轮 turn 结束时 | 模型确认条件已满足 |
| Stop hook | 上一轮 turn 结束时 | 你自己的脚本 / prompt 决定 |

要**按时间轮询**用 `/loop`；要让会话**持续工作到某个条件满足**用 `/goal`；要**每轮结束时**做点事用 Stop hook。

## 7. 最佳实践

要充分发挥 Claude Code 的潜力，掌握一些最佳实践是非常重要的。在本节中，我们将总结一些在使用 Claude Code 过程中被证明行之有效的技巧和策略。

### 7.1 优化设置（CLAUDE.md 文件）

**CLAUDE.md** 是一个特殊的 Markdown 文件，当 Claude Code 启动时会自动将其内容加载到上下文中。利用 `CLAUDE.md` 文件，你可以为 Claude Code 提供项目的背景信息和指导原则，使其更好地理解你的代码库和工作流程。

#### 放置位置：

你可以将 `CLAUDE.md` 文件放置在多个位置：

- **项目根目录：**最常见的方式，放在你运行 `claude` 命令的目录下。你可以将其命名为 `CLAUDE.md` 并提交到仓库，与团队共享；或者命名为 `CLAUDE.local.md` 并加入 `.gitignore`，仅供个人使用。
- **父目录：**也可以放在你运行 `claude` 的目录的任何父目录中。这在 monorepo 结构中很有用。
- **子目录：**放在运行 `claude` 目录的子目录中。当你进入某个子目录工作时，Claude Code 会按需读取该子目录的 `CLAUDE.md`。
- **用户主目录：**放在 `~/.claude/CLAUDE.md`，这会将该指导应用到所有的 Claude Code 会话。

#### 内容建议：

在 `CLAUDE.md` 文件中，你可以包含以下内容：

- **常用命令：**列出项目中常用的构建、测试、部署命令及其用途。例如：
  - `npm run build`：构建项目
  - `npm run test`：运行测试
- **代码风格：**说明项目的编码规范和风格指南。例如：
  - 使用 ES 模块语法，不要使用 CommonJS
  - 尽量解构导入
- **工作流程：**描述团队的工作流程和约定。例如：
  - 在完成一系列代码修改后，记得运行类型检查
  - 优先运行单个测试，而非整个套件，以提高性能
- **环境设置：**说明项目所需的开发环境配置。例如：
  - 使用 pyenv 切换 Python 版本
  - 需要 Node.js 版本 18 以上
- **其他信息：**任何你认为 Claude Code 需要知道的信息，例如特殊的行为、已知的警告、项目结构解释等。

#### 动态改进：

`CLAUDE.md` 文件就像一份不断演进的提示词，你应该根据实际使用情况不断改进它。一个常见的错误是添加了大量内容但从未验证其效果。你可以通过在对话中按 `#` 键快速将当前对话内容加入到 `CLAUDE.md` 中，方便你随时记录有用的命令或指导。

#### 最佳实践：

- **保持简洁：**尽量将 `CLAUDE.md` 写得简洁明了，突出重点。冗长的提示可能占用过多 token 并降低效率。
- **结构清晰：**使用标题、列表等 Markdown 格式使 `CLAUDE.md` 易读易维护。
- **团队共享：**将通用的项目信息放在提交到仓库的 `CLAUDE.md` 中，将个人偏好放在本地的 `CLAUDE.local.md` 中。
- **版本控制：**将 `CLAUDE.md` 纳入版本控制，同时通过 `.gitignore` 排除 `CLAUDE.local.md`。

> 💡 **回顾第 2 章**：`CLAUDE.md` 里的内容只是模型"尽量遵循"的**软约束**。真正"必须发生"的规则（如禁止删除某些文件、强制运行测试）应写进 **hooks 或权限规则**（harness 强制执行），才不会被违背。

### 7.2 明确具体地提出请求

与 Claude Code 交互时，清晰而具体地提出请求能够显著提高其输出质量。

#### 示例对比：

- 不好的请求：`"修复这个 bug"`。过于笼统，Claude Code 可能不知道从何入手。
- 好的请求：`"修复登录 bug：用户输入错误凭证后看到空白屏幕"`。提供了上下文和具体现象。

#### 提供上下文：

在请求中包含相关的上下文信息（错误信息、预期行为、相关文件名等）。例如不要只说"优化这个函数"，而说"优化这个函数以提高性能，它目前处理大数据时很慢"。

#### 使用步骤式指令：

对于复杂任务，将其分解为若干步骤，并逐步引导 Claude Code 完成：
```text
> 1. 创建一个新的数据库表来存储用户资料
> 2. 创建一个 API 端点来获取和更新用户资料
> 3. 创建一个网页界面让用户查看和编辑自己的资料
```

#### 避免歧义：

尽量使用明确的语言。例如不要说"让它快一点"，而说"将响应时间从 200ms 降低到 50ms 以下"。

### 7.3 分步指导复杂任务

对于复杂的任务，将其分解为多个小步骤并逐步指导 Claude Code 完成是一种有效策略。

#### 逐步验证：

每完成一步，就让 Claude Code 运行相应的测试或检查，确保这一步没有引入问题，然后再进入下一步。这种逐步验证的方式可以及早发现问题。

#### 反馈循环：

在每一步完成后查看输出并提供反馈。如果不符合预期，指出问题让 Claude Code 修正，然后再进入下一步。

#### 使用斜杠命令：

如果你发现某类复杂任务经常需要分步完成，可以考虑将其封装成一个自定义斜杠命令。

分步指导复杂任务的核心思想是"化整为零，逐步逼近"。

### 7.4 先让 Claude 探索

在让 Claude Code 开始编码之前，先让它对代码库进行探索和理解，是一种值得推荐的做法。

#### 提出探索性问题：

```text
> 分析数据库模式，找出所有与用户相关的表
> 概述项目的认证流程
> 找出所有调用了外部 API 的地方
```

#### 使用 Plan 模式：

Plan 模式非常适合用于代码探索——在只读状态下让 Claude Code 分析代码库或设计方案，不会修改任何文件。

#### 建立心智模型：

通过让 Claude Code 先探索，它可以建立项目的"心智模型"，当它开始执行具体任务时，就能利用这个模型做出更合理的决策。

### 7.5 使用快捷键

Claude Code 提供了一些快捷键，可以让你在交互时更加高效。按 `?` 键可查看所有可用快捷键。常用快捷键：

- `Tab`：命令自动补全。
- `↑` / `↓`：浏览命令历史。
- `Shift+Tab`：循环切换权限模式（`default` → `acceptEdits` → `plan`）。
- `Ctrl+C`：中断当前命令。
- `Ctrl+D`：退出 Claude Code（相当于 `/exit`）。
- `#`：将当前对话内容添加到 `CLAUDE.md`。

> **关于自定义快捷键**：Claude Code 本身支持通过 `~/.claude/keybindings.json` 自定义键位绑定（可用 `/keybindings-help` 技能查看说明）。

### 7.6 利用 Plan 模式减少风险

**Plan 模式**是一个非常有用的工具，可以帮助你在执行高风险或大规模的代码变更前进行周密的计划和审查。

#### 降低风险：

Plan 模式确保 Claude Code 不会对文件做任何修改，因此你可以放心地让它尝试各种方案，而不必担心破坏代码。

#### 全面审查：

在 Plan 模式下，Claude Code 会提供详细的计划和推理过程。你可以仔细审查每一步计划，确保没有遗漏或错误。

#### 明确需求：

Plan 模式鼓励 Claude Code 提出澄清问题，这有助于你在编码前明确需求，在早期消除模糊之处。

#### 版本控制友好：

由于 Plan 模式不产生提交，你可以放心地进行多次尝试和讨论。当你最终确定方案并切换到 `default` / `acceptEdits` 模式执行时，产生的提交才是清晰且有意义的。

总之，Plan 模式是安全地探索和规划的利器。在涉及不确定因素或高风险的修改时，善用 Plan 模式可以让你更有信心地推进工作。

### 7.7 为敏感数据使用 MCP

在处理敏感数据（例如数据库、私有 API）时，使用 MCP（Model Context Protocol）服务器是比直接命令行工具更安全的选择。MCP 允许你封装对敏感数据的访问，并通过细粒度的权限控制来确保只有经过授权的操作才能执行。

#### 封装敏感操作：

通过 MCP，你可以将访问敏感数据库或服务的逻辑封装在一个专门的服务器中。Claude Code 只能调用 MCP 服务器提供的工具，而不能直接执行任意的 SQL 或 API 请求。

#### 细粒度权限控制：

MCP 服务器可以实现复杂的权限策略。例如，只允许 Claude Code 读取最近一个月的日志，或者只能在测试环境中修改数据。

#### 审计和日志：

由于所有对敏感数据的访问都经过 MCP 服务器，你可以在服务器端记录详细的日志和审计信息。

#### 降低提示注入风险：

使用 MCP 可以降低提示注入风险，因为 MCP 服务器可以验证和过滤 Claude Code 发来的请求。

### 7.8 使用 CLI 工具而非 MCP

与上一条相反，对于**非敏感**数据或一般性的任务，直接使用命令行工具往往比通过 MCP 更简单直接。

#### 减少复杂性：

使用 CLI 意味着你无需编写额外的 MCP 服务器代码。Claude Code 可以直接调用系统中的任何命令。

#### 性能与灵活性：

直接调用 CLI 通常比通过 MCP 调用要快（少了中间服务器这一层），且命令行工具种类繁多，几乎涵盖开发工作的方方面面。

#### 何时用哪个：

简单、非敏感的任务可以直接用 CLI；复杂、敏感或需要细粒度控制的任务则应考虑 MCP。在实际工作中，两者结合使用，以兼顾效率和安全性。

### 7.9 团队协作标准化

在团队环境中使用 Claude Code，制定一些标准和最佳实践是非常有益的。

#### 共享配置：

将团队通用的配置放入项目的 `.claude` 目录中，并通过版本控制共享。这包括 `settings.json`、`CLAUDE.md`、自定义斜杠命令、钩子脚本等。

#### 规范权限策略：

在团队的配置中明确允许和禁止的操作。例如，所有成员都禁止不经确认直接删除文件。

#### 标准化工作流：

制定常见任务的团队工作流程，通过共享的自定义命令来强制这些流程。

#### 代码审查与反馈循环：

在代码审查中也可以审查是否遵循了团队的使用规范。定期收集团队反馈，持续优化配置和策略。

### 7.10 持续学习和实验

最后，保持学习和实验的心态。Claude Code 是一个不断发展的工具，新的功能和改进会不断推出。

#### 关注官方更新：

定期查看官方文档和更新日志，了解新功能和变化。

#### 分享和交流：

加入社区，分享你的使用心得和遇到的问题。

#### 从错误中学习：

如果在使用过程中犯了错，把它当作学习机会，思考如何改进提示或配置。

#### 适应变化：

随着你或团队的成长，工作需求可能会变化，相应地调整配置和工作流程。

## 8. 故障排除

在使用 Claude Code 的过程中，你可能会遇到一些常见的问题。本节针对一些常见错误和异常情况提供排查思路和解决方案。

### 8.1 安装相关问题

#### 问题：

在 Windows 的 WSL 环境下安装时遇到错误，或安装后找不到 `claude` 命令。

#### 原因：

这可能是由于 WSL 环境配置不当或环境变量未设置导致的。

#### 解决：

确保在 WSL 中使用 Linux 版本的 Node.js 和 npm（通过 `which node` 检查，若指向 `/mnt/c/` 开头说明用了 Windows 的 Node）。推荐使用官方原生安装脚本（见 3.1），它会安装到 `~/.local/bin/claude`。确保该目录在 PATH 中：`export PATH="$HOME/.local/bin:$PATH"`（加入 `~/.bashrc` 或 `~/.zshrc` 永久生效）。Windows 原生安装则检查 `%USERPROFILE%\.local\bin` 是否在系统 PATH 中。

#### 问题：

安装时提示找不到命令或权限被拒绝。

#### 解决：

推荐使用官方原生安装脚本（见 3.1），它不需要 sudo，也不会遇到 npm 相关的路径问题。如果已通过 npm 安装失败，可尝试删除 `node_modules` 重新安装，或用 `npm config set prefix` 设置可写前缀路径。

#### 问题：

安装成功，但运行 `claude` 时提示"command not found"。

#### 解决：

检查 `claude` 安装位置（原生安装在 `~/.local/bin/claude` 或 `%USERPROFILE%\.local\bin\claude.exe`），确保该目录在 PATH 中。添加后重新打开终端或 `source ~/.bashrc` 使其生效，然后 `claude --version` 验证。

### 8.2 权限与认证问题

#### 问题：

Claude Code 频繁要求你确认同一个命令的执行权限，即使你之前已经选择过"Always allow"。

#### 解决：

运行 `/permissions` 命令查看当前的允许列表，确认期望的命令是否在其中。如果不在，可用 `/permissions` 添加（例如 `/permissions allow Edit`）。若使用团队共享配置，确保该命令在团队配置中没有被禁用。也可能是多个配置文件相互覆盖（例如全局允许但项目禁用）。

#### 问题：

Claude Code 提示认证失败或无法登录。

#### 解决：

确保你的 Claude 订阅或 Console 账户有效且有额度。如果使用 Console 账户，检查 API 密钥是否正确且未过期。可以尝试重新登录：运行 `/logout` 退出当前账户，然后重新运行 `claude` 按提示登录。若仍无法登录，检查网络连接；必要时删除本地认证缓存后重新登录。

#### 问题：

Claude Code 提示权限不足，无法执行某命令。

#### 解决：

运行 `/permissions` 查看哪些命令被禁用或需要确认。检查 `settings.json` 中的 `permissions` 部分，确认没有误将常用工具列入拒绝列表。注意：在 `plan` 模式下所有写操作默认被禁止，请切换到 `default` 或 `acceptEdits` 模式。

### 8.3 配置文件问题

#### 问题：

Claude Code 没有按照预期的配置工作，例如没有加载某个自定义斜杠命令，或者权限设置未生效。

#### 解决：

确认配置文件位置：用户全局配置在 `~/.claude/` 目录下，项目配置在项目根目录的 `.claude/` 目录下。检查文件名是否正确（`settings.json` 而不是 `setting.json`）。检查 JSON 格式是否正确（**代码块中的引号必须是英文半角，不能是中文全角引号**；不能多 / 少逗号）。

配置合并优先级（从高到低）：**managed（企业托管）> 命令行参数 > 项目本地 `settings.local.json` > 项目共享 `settings.json` > 用户 `~/.claude/settings.json`**。确保没有高优先级配置覆盖了你期望的设置。可用 `/config` 查看当前生效的配置值。

#### 问题：

钩子（Hooks）没有按照预期执行。

#### 解决：

确认钩子配置在 **`settings.json` 的 `hooks` 字段**中（不是独立的 `hooks.json` 文件）。检查三层嵌套结构是否正确（`事件 → matcher 组数组 → hooks handler 数组`），事件名拼写正确（是 `SessionStart` 不是 `OnSessionStart`）。检查钩子脚本路径是否正确、是否有执行权限。可以先配置一个简单的 `echo` 命令验证钩子机制本身是否工作。注意：在 `plan` 模式下不会触发写操作相关的钩子。

#### 问题：

自定义斜杠命令没有出现在命令列表中。

#### 解决：

确认命令文件位置（项目命令在 `.claude/commands/`，个人命令在 `~/.claude/commands/`），文件名以 `.md` 结尾。检查文件内容是否为有效的 Markdown。可以先写一个简单的"Hello"测试，确认机制本身工作。

### 8.4 性能与稳定性问题

#### 问题：

Claude Code 运行时占用 CPU 或内存过高。

#### 解决：

- **限制上下文范围**：限定 Claude Code 需要关注的文件和目录范围。
- **关闭不必要的功能**：暂时禁用导致资源占用高的 MCP 服务器或插件。
- **使用更轻量的模型**：在 `settings.json` 中选择更快的模型（如 Haiku 对应的 GLM-4.5-Air）。
- **分批处理**：对非常大的任务分批进行。
- **更新版本**：运行 `claude update` 更新到最新版本。

#### 问题：

Claude Code 命令执行时长时间无响应（挂起）。

#### 解决：

确认是否 Claude Code 在等待你确认操作（`default` 模式下执行命令前会征求许可）。检查终端输出看是否有确认提示。如果没有提示但一直挂起，可能是网络请求超时，可按 `Ctrl+C` 中断后重试。

#### 问题：

Claude Code 崩溃或异常退出。

#### 解决：

尝试重启 Claude Code。如果频繁崩溃，检查系统日志。若使用最新版本仍有问题，可尝试回退到之前的稳定版本。必要时使用 `/bug` 命令提交 Bug 报告（`/feedback` 的别名）。

### 8.5 搜索与发现相关问题

#### 问题：

Claude Code 在 WSL 环境下搜索或读取文件时速度很慢。

#### 解决：

WSL 在访问 Windows 文件系统时性能可能较差。尽量将项目代码放在 Linux 文件系统（例如 WSL 的 `~/` 目录下），而不是 Windows 的 `C:\` 盘。也可以考虑使用原生 Linux 环境而非 WSL。

#### 问题：

Claude Code 找不到某个文件或代码。

#### 解决：

确认文件路径是否正确。在对话中可以使用 `@filename` 语法明确指定某个文件（例如 `@src/utils/helpers.js`），让 Claude Code 读取该文件。检查项目的 `.gitignore` 或 Claude Code 的配置，确认没有忽略该文件。可以尝试 `/clear` 清除对话历史后重新询问。

### 8.6 IDE 集成相关问题

#### 问题：

在 JetBrains IDE 中安装了 Claude Code 插件，但插件无法正常工作。

#### 解决：

首先确保 Claude Code 本身可以在终端中正常运行（`claude --version` 有版本号输出）。然后在 IDE 中检查插件的设置，确保 Claude Code 可执行文件路径或监听端口配置正确。必要时重启 IDE 和 Claude Code，或查看 IDE 的插件日志。

#### 问题：

在 JetBrains IDE 的终端中使用 Claude Code 时，某些快捷键（如 Esc 键）不起作用。

#### 解决：

这通常是由于 IDE 终端的键映射设置与 Claude Code 的快捷键冲突。在 Settings > Keymap 中搜索冲突的快捷键并调整。

#### 问题：

Claude Code 在集成终端中显示乱码或不支持某些 Unicode 字符。

#### 解决：

确保终端使用 UTF-8 编码。在 Linux/macOS 上可在 `~/.bashrc` 或 `~/.zshrc` 中添加 `export LANG=en_US.UTF-8`。Windows 上推荐使用 Windows Terminal。

### 8.7 其他问题

#### 问题：

Claude Code 输出的代码块缺少语言标签或格式不正确。

#### 解决：

如果代码块很长，可以让 Claude Code 分段输出，或使用 `/compact` 精简对话历史以减少 token 占用。也可以明确提示"使用 Python 输出代码块"帮助识别语言。

#### 问题：

Claude Code 的提示信息显示不完整或有乱码。

#### 解决：

确保终端使用 UTF-8 编码并使用支持 Unicode 的字体。必要时更新 Claude Code 到最新版本。

在遇到任何未列出的问题时，请记住 **"大多数 Claude Code 问题都有简单的解决方案"**。先从基础开始检查：重启 Claude Code、检查命令路径和权限、确认网络和账户状态。如果这些基本步骤都无法解决，再考虑更深入的调查。

## 9. 总结

Claude Code 作为一款智能的命令行编程助手，正日益成为开发者不可或缺的伙伴。它不仅能够执行繁琐的日常任务，还能解释复杂的代码逻辑、管理 Git 工作流程，甚至主动提问来澄清需求，从而让编程工作变得前所未有的高效和轻松。

在本教程中，我们全面介绍了 Claude Code 的核心架构（模型与 Harness 的分工）、安装配置、基本使用流程、常见工作流程，以及高级功能和最佳实践。从理解"harness 负责执行与管控、模型负责推理"这一根本架构，到快速启动一个会话，再到使用斜杠命令、钩子和循环定时任务定制你的工作流，最后利用 MCP 连接外部工具，我们逐步深入，帮助你构建对 Claude Code 的完整认识。

Claude Code 的强大之处在于其灵活性和可扩展性。无论你是个人开发者还是团队成员，都可以根据自己的需求定制 Claude Code。通过遵循本教程介绍的最佳实践——尤其是区分"软约束（CLAUDE.md 提示）"和"硬约束（hooks / 权限规则，由 harness 强制执行）"——你可以最大限度地发挥 Claude Code 的潜力，同时保持对代码质量和安全性的掌控。

当然，掌握 Claude Code 也是一个持续学习和实验的过程。随着新功能和改进不断推出（例如本教程涉及的 GLM-5.2 模型、`/effort` 思考强度、循环定时任务等），以及你自身项目的演进，你可能会发现新的用法和优化空间。保持开放的心态，尝试不同的配置和工作流，并从社区中汲取经验。

总之，Claude Code 将 AI 的智能带入了编程的日常，使"像与同事对话一样编码"成为现实。通过本教程的学习，相信你已经具备了在自己的项目中熟练使用 Claude Code 的能力。现在，就打开终端，启动 Claude Code，开始享受它为你带来的编程变革吧！祝你编码愉快，创意无限！
