# README 创建指南

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

## 组件 README 创建标准

不是每个组件都需要 README，根据复杂度判断。

### 需要 README（满足任一）

| 维度 | 触发条件 |
|------|----------|
| API 复杂度 | props/slots/事件 ≥6，或有互斥配置组合 |
| 使用风险 | 存在已知陷阱（受控/非受控、SSR、性能等） |
| 交互复杂度 | 键盘/焦点管理、拖拽、异步加载、动画 |
| 外部依赖 | 依赖上下文、Provider 或浏览器 API |

### 不需要 README

- 简单展示型组件（`Badge`、`Divider`）
- API ≤3 且无状态/副作用
- 已被全局文档或 Storybook 覆盖

## 无 README 时的注释要求

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
