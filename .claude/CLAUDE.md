# AI Workflow Skills

通用 AI 编码助手技能集合。

## 项目概述

本仓库提供可在多种 AI 编码工具间复用的模块化技能。

### 支持的工具及 Skill 目录

| 工具              | 项目级目录          | 全局目录                     |
| ----------------- | ------------------- | ---------------------------- |
| Claude Code       | `.claude/skills/`   | `~/.claude/skills/`          |
| OpenAI Codex CLI  | `.codex/skills/`    | `~/.codex/skills/`           |
| Google Gemini CLI | `.gemini/skills/`   | `~/.gemini/skills/`          |
| OpenCode          | `.opencode/skills/` | `~/.config/opencode/skills/` |

> OpenCode 也支持读取 `.claude/skills/` 目录

## 技能列表

| 技能              | 描述                                                   |
| ----------------- | ------------------------------------------------------ |
| `git-commit`      | 专业的 git 提交工作流，自动分析变更并生成提交信息      |
| `codex`           | 使用 OpenAI Codex CLI 进行代码审查与分析               |
| `aidoc`           | AI 友好的文档管理，支持渐进式披露                      |
| `initial-project` | 项目初始化，配置常用工具（Prettier、ESLint、Husky 等） |

## 安装方式

可使用 Vercel 的 `add-skill` 包安装：

```bash
npx add-skill <skill-url>
```

或手动复制 `SKILL.md` 到项目中。

## 开发指南

### 添加新技能

1. 在 `skills/` 下创建新目录
2. 按照 [skill-format.md](doc/skill-format.md) 规范编写 `SKILL.md`
3. 更新本文件和 `README.md`
