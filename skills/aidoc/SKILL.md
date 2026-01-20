---
name: aidoc
description: 当用户请求更新文档、整理文档时触发。项目文档整理与更新，实现 AI 友好的渐进式披露。
---

# AI 文档整理与更新

> 用户输入 `/aidoc` 时触发。软触发提醒由 `git-commit` skill 负责。

## 概述

维护项目的 AI 配置文件和组件 README，确保文档结构清晰、信息单一来源、避免重复。

## 文档层级与职责

| 文档 | 职责 | 内容 |
|------|------|------|
| `README.md` | 项目入口 | 介绍、安装、使用（单一信息源） |
| AI 配置文件 | AI 协作指引 | 开发规范、维护指南（引用 README） |
| 组件 README | 模块说明 | 仅该组件特有的陷阱、模式 |
| `doc/` | 详细文档 | 外链的完整列表、深度指南 |

**AI 配置文件对照：**

| 工具 | 文件 |
|------|------|
| Claude Code | `CLAUDE.md` 或 `.claude/CLAUDE.md` |
| Codex CLI | `AGENTS.md` |
| Gemini CLI | `GEMINI.md` |
| OpenCode | `AGENTS.md` 或 `.opencode/AGENTS.md` |

### 组件 README 创建标准

不是每个组件都需要 README，根据复杂度判断。

**需要 README（满足任一）：**

| 维度 | 触发条件 |
|------|----------|
| API 复杂度 | props/slots/事件 ≥6，或有互斥配置组合 |
| 使用风险 | 存在已知陷阱（受控/非受控、SSR、性能等） |
| 交互复杂度 | 键盘/焦点管理、拖拽、异步加载、动画 |
| 外部依赖 | 依赖上下文、Provider 或浏览器 API |

**不需要 README：**
- 简单展示型组件（`Badge`、`Divider`）
- API ≤3 且无状态/副作用
- 已被全局文档或 Storybook 覆盖

**无 README 时的注释要求：**

组件文件头部应包含：

```typescript
/**
 * 组件名称 - 一句话描述
 *
 * @example
 * <Component prop="value" />
 *
 * @note 特殊约束或注意事项（如有）
 */
```

复杂函数/hook 需补充：
- `@param` - 参数说明（非显而易见时）
- `@returns` - 返回值说明
- `@throws` - 可能的异常（如有）

## 核心原则

### 避免重复（DRY）

1. **引用而非复制** - 通用信息放 README，配置文件用 `> 详见 README` 引用
2. **单一信息源** - 每项信息只在一处维护
3. **就近原则** - 组件相关陷阱放组件 README

### 渐进式披露

- 配置文件只保留核心信息
- 详细内容外链到 `doc/` 或组件 README
- 阈值：>200 行建议外链，>300 行必须外链

详见 [outlink-strategy.md](references/outlink-strategy.md)

> 理论基础参考 [agentic-coding-guide.md](references/agentic-coding-guide.md)

## 执行步骤

### 第一步：评估现状

```bash
# 检查配置文件行数
wc -l CLAUDE.md AGENTS.md 2>/dev/null

# 查看 fix/refactor 提交（可能产生陷阱/模式）
git log --oneline --grep="fix:" --grep="refactor:" --since="1 month ago"
```

### 第二步：检查重复

- 配置文件是否复制了 README 内容？→ 改为引用
- 通用陷阱是否堆积在根配置文件？→ 外链或就近

### 第三步：更新文档

根据本次修改：

1. **新增功能** → 更新 README 功能列表
2. **fix 提交** → 评估是否记录到「已知陷阱」
3. **refactor 提交** → 评估是否产生「成功模式」
4. **组件修改** → 检查组件 README 是否需要更新

### 第四步：验证结构

- [ ] 配置文件 <200 行（或已合理外链）
- [ ] 无重复内容（引用而非复制）
- [ ] 陷阱/模式就近存放
