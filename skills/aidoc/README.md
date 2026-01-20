# aidoc

AI 友好的文档管理技能，支持渐进式披露。

## 功能

- 优化 AI 配置文件结构
- 从 git 历史提取陷阱和模式
- 检查文档层级是否合理
- 更新组件 README

## 触发词

- `/aidoc`
- `更新文档`
- `整理文档`

## 安装

```bash
npx add-skill https://github.com/user/ai-workflow/tree/main/skills/aidoc
```

## 支持的 AI 配置文件

| 工具 | 配置文件 |
|------|----------|
| Claude Code | `CLAUDE.md` |
| OpenAI Codex CLI | `AGENTS.md` |
| Google Gemini CLI | `GEMINI.md` |
| OpenCode | `AGENTS.md` |

## 外链策略

当配置文件过长时自动建议外链：

| 阈值 | 条件 | 动作 |
|------|------|------|
| 软阈值 | >200 行 或 陷阱+模式 >12 条 | 建议外链 |
| 硬阈值 | >300 行 | 必须外链 |
