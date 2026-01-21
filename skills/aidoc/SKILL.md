---
name: aidoc
description: 当用户请求更新文档、整理文档时触发。项目文档整理与更新，实现 AI 友好的渐进式披露。
---

# AI 文档整理与更新

> 用户输入 `/aidoc` 时触发。软触发提醒由 `git-commit` skill 负责。

## 概述

维护项目的 AI 配置文件和 README，确保文档结构清晰、信息单一来源、避免重复。

## 执行步骤

### 第一步：询问用户意图

询问用户想要执行的任务（可多选）：

| 选项 | 说明 | 是否修改 |
|------|------|:--------:|
| **健康检查**（默认） | 诊断报告：重复、行数、README 需求评估 | ❌ |
| **更新配置文件** | 更新 CLAUDE.md/AGENTS.md 等 AI 配置 | ✅ |
| **README 管理** | 评估并创建/更新项目或组件 README | ✅ |
| **项目初始化** | 为新项目创建完整文档结构 | ✅ |
| **基于最近提交** | 针对 fix/refactor 记录陷阱/模式 | ✅ |

**默认行为**：若用户未指定，执行「健康检查」并输出建议动作清单。

### 第二步：评估现状

```bash
# 检查配置文件行数
wc -l CLAUDE.md AGENTS.md 2>/dev/null

# 查看 fix/refactor 提交（可能产生陷阱/模式）
git log --oneline --grep="fix:" --grep="refactor:" --since="1 month ago"
```

**健康检查输出项：**
- 配置文件行数是否超标（>200 行）
- 是否存在重复内容（配置文件复制 README）
- 项目 README 是否需要更新
- 组件 README 需求评估（需要/不需要/待定）

### 第三步：执行任务

**更新配置文件：**
- 检查并修复重复内容（改为引用）
- 执行外链策略（>200 行外链）

**README 管理：**
- 项目 README：更新功能列表、安装说明
- 组件 README：根据复杂度标准创建/更新（详见 [readme-guidelines.md](references/readme-guidelines.md)）

**项目初始化：**
- 创建 README.md + AI 配置文件 + `doc/` 目录

**基于最近提交：**
- fix → 评估是否记录「已知陷阱」
- refactor → 评估是否产生「成功模式」

### 第四步：验证与汇报

- [ ] 配置文件 <200 行（或已合理外链）
- [ ] 无重复内容（引用而非复制）
- [ ] 陷阱/模式就近存放

## 核心原则

### 避免重复（DRY）

1. **引用而非复制** - 通用信息放 README，配置文件用引用
2. **单一信息源** - 每项信息只在一处维护
3. **就近原则** - 组件相关陷阱放组件 README

### 渐进式披露

- 配置文件只保留核心信息
- 阈值：>200 行建议外链，>300 行必须外链

详见 [outlink-strategy.md](references/outlink-strategy.md)

## 参考文档

| 文档 | 内容 |
|------|------|
| [readme-guidelines.md](references/readme-guidelines.md) | README 创建标准与注释规范 |
| [outlink-strategy.md](references/outlink-strategy.md) | 外链策略详解 |
| [agentic-coding-guide.md](references/agentic-coding-guide.md) | AI 协作理论基础 |
