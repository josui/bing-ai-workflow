# AI Workflow

通用 AI 编码助手技能集合，可在多种 AI 工具间复用。

## 支持的 AI 工具

| 工具                                                             | 项目级 Skill 目录   | 全局 Skill 目录              |
| ---------------------------------------------------------------- | ------------------- | ---------------------------- |
| [Claude Code](https://claude.ai/claude-code)                     | `.claude/skills/`   | `~/.claude/skills/`          |
| [OpenAI Codex CLI](https://github.com/openai/codex)              | `.codex/skills/`    | `~/.codex/skills/`           |
| [Google Gemini CLI](https://github.com/google-gemini/gemini-cli) | `.gemini/skills/`   | `~/.gemini/skills/`          |
| [OpenCode](https://github.com/opencode-ai/opencode)              | `.opencode/skills/` | `~/.config/opencode/skills/` |

> OpenCode 也支持读取 `.claude/skills/` 目录

## 技能列表

| 技能                                         | 描述                                                    | 触发词                           |
| -------------------------------------------- | ------------------------------------------------------- | -------------------------------- |
| [git-commit](./skills/git-commit/)           | 专业的 git 提交工作流，自动分析变更并生成规范的提交信息 | `/commit`、`提交代码`            |
| [codex](./skills/codex/)                     | 使用 OpenAI Codex CLI 进行代码审查与分析                | `/codex`、`代码审查`             |
| [aidoc](./skills/aidoc/)                     | AI 友好的文档管理，支持渐进式披露原则                   | `/aidoc`                         |
| [initial-project](./skills/initial-project/) | 项目初始化，配置 Prettier、ESLint、Husky 等常用工具     | `/initial-project`、`初始化项目` |

## 安装方式

### 方式一：使用 add-skill（推荐）

[add-skill](https://github.com/vercel-labs/agent-skills) 是 Vercel 提供的技能安装工具，支持多种 AI 编码工具。

```bash
# 安装单个技能
npx add-skill https://github.com/user/bing-ai-workflow/tree/main/skills/git-commit

# 根据当前使用的工具自动选择配置文件
```

### 方式二：手动安装

1. 复制对应技能目录（包含 `SKILL.md`）
2. 根据使用的 AI 工具，放入对应的 skill 目录：
   - Claude Code → `.claude/skills/`
   - Codex CLI → `.codex/skills/`
   - Gemini CLI → `.gemini/skills/`
   - OpenCode → `.opencode/skills/`

## 相关资源

- [Vercel Agent Skills](https://github.com/vercel-labs/agent-skills) - 技能安装工具
- [Claude Code 文档](https://docs.anthropic.com/claude-code)
- [Codex CLI 文档](https://developers.openai.com/codex/cli/)
- [Gemini CLI 文档](https://geminicli.com/docs/)
- [OpenCode 文档](https://opencode.ai/docs/)

## 许可证

MIT
