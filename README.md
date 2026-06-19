# Claude Code 完整教程

欢迎使用 Claude Code 完整教程！本教程集合包含从入门到精通的全部学习资料，帮助你掌握 Claude Code 智能编程助手的使用方法，并学会用 **Skills** 为 AI 助手扩展可复用的专业能力。

## 📖 教程简介

本教程包含两大核心内容：

- **Claude Code 使用手册**：Claude Code 的完整使用教程，涵盖架构理解、安装配置、基础使用、高级功能与最佳实践。既提供[按章节拆分版](./Claude%20Code/README.md)，也保留[单文件完整版](./Claude%20Code/Claude%20Code%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.md)。
- **Skills 指南**：讲清楚 Skills（可复用的程序性知识包）的概念、`SKILL.md` 结构、如何创建自己的技能，以及如何通过 [Skills.sh](https://www.skills.sh/) 发现与安装社区技能。

## 📚 阅读顺序

### 第一步：Claude Code 使用手册

**入口**：[章节索引](./Claude%20Code/README.md) ｜ [单文件版](./Claude%20Code/Claude%20Code%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C.md)

适合人群：Claude Code 初学者和希望系统学习的用户

主要内容：
- 理解 Claude Code 架构（模型与 Harness 的分工）
- 安装与配置（含 GLM Coding Plan、GLM-5.2 模型）
- 基础使用流程与常见工作流
- 高级功能（斜杠命令、钩子、插件与 MCP、Plan 模式、循环定时任务）
- 最佳实践与故障排除

**学习目标**：掌握 Claude Code 的基础操作和核心功能，在实际开发中高效使用。

---

### 第二步：Skills 指南

**入口**：[Skills/README.md](./Skills/README.md)

适合人群：希望为 AI 助手扩展专业能力的开发者

主要内容：
- Skills 是什么，以及渐进式披露的工作机制
- `SKILL.md` 的完整结构与 frontmatter 字段
- 从零创建一个自己的 Skill（实战）
- 通过 Skills.sh 发现与安装社区技能
- Skills 与 MCP、插件的区别

**学习目标**：学会创建和管理 Skills，把团队的流程与规范沉淀成可复用的能力。

---

## 🚀 快速开始

1. **第一次用**？从 [Claude Code 使用手册](./Claude%20Code/README.md) 开始
2. **想扩展能力**？阅读 [Skills 指南](./Skills/README.md)
3. **想找现成技能**？去 [Skills.sh](https://www.skills.sh/) 浏览社区技能

## 📂 目录结构

```
Claude Code/
├── Claude Code/                    # Claude Code 使用教程
│   ├── README.md                   # 教程索引（章节导航）
│   ├── Claude Code使用手册.md       # 单文件完整版
│   └── 章节/                       # 按章节拆分（共 9 个文件）
│       ├── 01-简介.md
│       ├── 02-架构与Harness.md
│       └── ...
├── Skills/                         # Skills 技能指南
│   ├── README.md                   # Skills 完整指南
│   └── img/                        # 配图
├── LICENSE                         # MIT 开源协议
└── README.md                       # 本文件
```

## 💡 学习建议

- **循序渐进**：按推荐顺序学习，先掌握 Claude Code 本体，再深入 Skills。
- **实践结合**：边读边动手，真正创建几个 Skill 试试。
- **持续迭代**：Skills 可不断改进，根据使用反馈持续优化。
- **社区交流**：关注 [Skills.sh](https://www.skills.sh/) 获取最新技能与动态。

## 🔗 相关资源

- [Claude Code 官方文档](https://code.claude.com/docs)
- [Skills.sh — 开放 agent skills 目录](https://www.skills.sh/)
- [GLM Coding Plan 文档](https://docs.bigmodel.cn/cn/coding-plan)

## 📜 开源协议

本教程采用 [MIT License](./LICENSE) 开源协议。

> 本项目允许任何人自由使用、修改和分发，只需在衍生作品中保留版权声明和许可声明。

---

**版本**：v2.0
**更新日期**：2026-06-20
**维护者**：zzy
**协议**：[MIT License](./LICENSE)
