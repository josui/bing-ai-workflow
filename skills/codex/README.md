# codex

使用 OpenAI Codex CLI 进行代码审查与分析。

## 功能

- 代码审查
- 全项目代码分析
- Bug 调查
- 重构建议
- 性能分析

## 触发词

- `/codex`
- `代码审查`
- `审查一下`
- `分析一下`

## 安装

```bash
npx add-skill josui/bing-ai-workflow -s codex
```

## 前置要求

需要安装 [OpenAI Codex CLI](https://github.com/openai/codex)：

```bash
npm install -g @openai/codex
```

## 使用示例

```bash
# 代码审查
codex exec --full-auto --sandbox read-only --cd /path/to/project "请审查该项目代码"

# Bug 调查
codex exec --full-auto --sandbox read-only --cd /path/to/project "请调查登录失败的原因"
```
