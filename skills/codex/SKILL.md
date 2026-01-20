---
name: codex
description: 当用户请求代码审查、审查一下、分析一下时触发。使用 OpenAI Codex CLI 进行代码审查、分析和问题调查。
---

# Codex

> 使用 Codex CLI 执行代码审查与分析的技能。

## 概述

当需要进行代码审查、全项目分析、Bug 调查或重构建议时触发此技能。通过 Codex CLI 在只读沙箱中安全执行分析任务。

## 适用场景

- 代码审查请求
- 全项目代码分析
- 实现方案咨询
- Bug 调查
- 重构建议
- 难以解决的问题调查

## 执行步骤

### 第一步：确认需求

从用户处获取具体需求：
- 审查/分析的目标
- 特定关注点（如性能、安全、可维护性）
- 目标项目目录

### 第二步：执行命令

```bash
codex exec --full-auto --sandbox read-only --cd <project_directory> "<request>"
```

### 第三步：反馈结果

将 Codex 的分析结果整理后反馈给用户。

## 命令参数

| 参数 | 说明 |
|------|------|
| `--full-auto` | 完全自动模式运行 |
| `--sandbox read-only` | 只读沙箱（用于安全分析） |
| `--cd <dir>` | 目标项目目录 |
| `"<request>"` | 需求内容（支持中文） |

## 示例

### 代码审查

```bash
codex exec --full-auto --sandbox read-only --cd /path/to/project "请审查该项目代码并指出改进点"
```

### Bug 调查

```bash
codex exec --full-auto --sandbox read-only --cd /path/to/project "请调查用户登录失败的原因"
```

### 性能分析

```bash
codex exec --full-auto --sandbox read-only --cd /path/to/project "分析项目中可能存在的性能瓶颈"
```
