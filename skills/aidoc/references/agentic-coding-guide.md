# Agentic Coding 最佳实践指南

> 来源：TRAE 字节跳动技术团队
> 作者：小夏
> 日期：2026-01-12
> 原文：https://mp.weixin.qq.com/s?__biz=MzI1MzYzMjE0MQ==&mid=2247517928

---

## 核心原则

### 1. 理解 LLM 本质

- **预测下一个 token**：LLM 没有独立思考过程，只是在预测最可能的下一个词
- **上下文即全部记忆**：窗口外的内容对 LLM 来说不存在
- **有效上下文有限**：实际有效利用的上下文远小于标称值（约 10-15%）
- **无状态**：每次对话都是全新开始，除非显式提供历史

### 2. 短对话优于长对话

- 每个对话只做一件事
- 对话越长，性能越差，成本越高
- 完成子任务后开始新对话
- 避免在单个对话中处理多个独立任务

### 3. 渐进式披露（Progressive Disclosure）

- 配置文件控制在 300 行以内
- 详细文档通过指针按需加载
- 不要让 Agent 做 Linter 的工作（用工程约束替代 prompt 指令）

### 4. 复利工程（Compound Interest Engineering）

- 将经验沉淀为可复用知识
- 记录已知陷阱和成功模式
- 每次 bug 修复都应防止同类问题再次发生

### 5. 对人难的事，对 AI 也难

- 好的文档帮助 AI 快速理解
- 快速的反馈循环（测试、构建）
- 清晰的代码结构和命名

---

## 渐进式披露实践

### 文档层级设计

```
Level 0: CLAUDE.md（<300行）
├── 项目概述
├── 重要规则（硬性约束）
├── 技术栈
├── 项目结构
├── 开发命令
├── 文档指针 → Level 1
├── 已知陷阱
└── 成功模式

Level 1: doc/ 目录（按需加载）
├── product/        # 产品规格
├── architecture/   # 架构设计
├── reference/      # 参考资料
└── plan/           # 开发计划

Level 2: 代码内 README（就近原则）
├── src/components/charts/README.md
├── src/components/editor/README.md
└── src/utils/README.md
```

### CLAUDE.md 模板示例

```markdown
# 项目名称

## 项目概述

一句话描述项目用途。

## 重要规则

- 硬性约束 1
- 硬性约束 2

## 技术栈

| 类别 | 选择  | 说明 |
| ---- | ----- | ---- |
| 框架 | React | ...  |

## 项目结构

src/
├── components/
├── utils/
└── types/

## 开发命令

pnpm dev # 开发
pnpm build # 构建
pnpm test # 测试

## 文档参考

详细文档按需查阅：

- `doc/product/` - 产品规格
- `doc/architecture/` - 架构设计

## 已知陷阱

| 问题     | 正确做法 | 来源        |
| -------- | -------- | ----------- |
| 问题描述 | 解决方案 | commit hash |

## 成功模式

- 模式 1：描述
- 模式 2：描述
```

---

## 复利工程实践

### 已知陷阱记录规范

每次修复 bug 后，评估是否需要记录：

1. **是否可能再犯？** - 如果是偶发的拼写错误，不需要记录
2. **是否有通用性？** - 如果只影响特定文件，可能不需要
3. **是否违反直觉？** - 如果正确做法不明显，应该记录

记录格式：

```markdown
| 问题                     | 正确做法                     | 来源        |
| ------------------------ | ---------------------------- | ----------- |
| 轴单位在某些条件下被隐藏 | 始终显示轴单位，不做条件判断 | fix: abc123 |
```

### 成功模式记录规范

当发现有效的代码组织或设计模式时记录：

```markdown
## 成功模式

- **组件拆分策略** - 参考 BarChart：common/ + HorizontalBars/ + VerticalBars/
- **样式统一** - 使用 `chartTextDefaults` 对象统一配置
- **常量管理** - 所有设计常量集中在 `src/design/`
```

---

## 工程约束替代 Prompt 指令

### 反模式：用 prompt 约束

```markdown
## 规则

- 不要使用 any 类型
- 所有函数必须有注释
- 变量命名使用 camelCase
```

问题：LLM 可能忘记或忽略这些规则

### 正模式：用工程工具约束

```json
// tsconfig.json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true
  }
}

// eslint.config.js
{
  "rules": {
    "@typescript-eslint/no-explicit-any": "error"
  }
}
```

好处：

- 立即反馈（编译/lint 报错）
- 无法绕过
- 不消耗 context

---

## 快速反馈循环

### 验证脚本示例

```bash
#!/bin/bash
# scripts/verify.sh - 快速验证脚本

set -e

echo "=== Type Check ==="
pnpm tsc --noEmit

echo "=== Lint ==="
pnpm lint

echo "=== Build ==="
pnpm build

echo "=== All checks passed ==="
```

在 CLAUDE.md 中引用：

```markdown
## 开发命令

pnpm verify # 运行所有检查（类型、lint、构建）
```

---

## 实践检查清单

### 每次开发会话前

- [ ] 确认 CLAUDE.md 是最新的
- [ ] 检查是否有相关的详细文档需要加载
- [ ] 明确本次会话的单一目标

### 每次 bug 修复后

- [ ] 评估是否需要记录到「已知陷阱」
- [ ] 考虑是否可以添加工程约束防止再犯
- [ ] 更新相关文档（如果影响使用方式）

### 每次功能完成后

- [ ] 评估是否有可复用的模式
- [ ] 更新相关 README（如果改变了组件用途）
- [ ] 确认文档与代码同步

---

## 参考资源

- 原文地址：https://mp.weixin.qq.com/s?__biz=MzI1MzYzMjE0MQ==&mid=2247517928
- Claude Code 官方文档：https://docs.anthropic.com/claude-code
- Cursor Rules 最佳实践：https://cursor.directory
