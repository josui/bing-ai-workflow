---
name: initial-project
description: 当用户请求初始化项目、配置开发环境时触发。配置 Prettier、ESLint、Husky、lint-staged 等常用工具。
---

# 项目初始化

> 用户输入 `/initial-project` 或 "初始化项目" 时触发。

## 概述

解决新项目启动时重复配置开发工具的痛点，提供一站式初始化方案。根据项目类型（React/Vue/Node.js 等）自动配置 Prettier、ESLint、Husky、lint-staged 等工具。

## 版本原则

**始终使用满足兼容性的最新稳定版本。**

执行前需确认各工具的版本兼容性：

1. **优先使用 MCP 工具查询**（如已安装）：
   - [ref.tools](https://ref.tools/) - 查询包版本和兼容性
   - context7 MCP - 获取最新文档和配置示例

2. **Web Search 调查**：
   - 不确定的版本搭配、配置语法变更
   - 框架特定的插件兼容性
   - 已知的 breaking changes

3. **关注点**：
   - ESLint 9.x Flat Config vs 旧版配置
   - TypeScript ESLint 8.x 的变化
   - 各框架插件的版本要求

## 核心工具清单

| 工具 | 用途 | 优先级 |
|------|------|--------|
| Prettier | 代码格式化 | 必选 |
| ESLint | 代码质量检查 | 必选 |
| Husky | Git hooks 管理 | 必选 |
| lint-staged | 暂存文件检查 | 必选 |
| commitlint | 提交信息规范 | 可选 |
| TypeScript | 类型检查 | 按需 |
| Stylelint | CSS/SCSS 规范 | 按需 |
| EditorConfig | 编辑器配置统一 | 推荐 |

## 执行步骤

### 第一步：确认项目信息

询问用户以下信息：

1. **包管理器**：npm / pnpm / yarn / bun
2. **框架类型**：React / Vue / Node.js / 纯 TypeScript / 其他
3. **样式方案**：CSS / SCSS / Tailwind / CSS-in-JS / 无
4. **TypeScript**：是否使用
5. **可选工具**：commitlint、Stylelint、EditorConfig

### 第二步：安装依赖

```bash
# 基础工具
pnpm add -D prettier eslint husky lint-staged

# ESLint 相关（根据框架选择，详见 references/frameworks.md）
pnpm add -D @typescript-eslint/parser @typescript-eslint/eslint-plugin

# 可选
pnpm add -D @commitlint/cli @commitlint/config-conventional
pnpm add -D stylelint stylelint-config-standard
```

### 第三步：创建配置文件

从 `assets/` 目录复制模板文件到项目根目录：

| 文件 | 用途 |
|------|------|
| [.prettierrc](assets/.prettierrc) | Prettier 配置 |
| [.prettierignore](assets/.prettierignore) | Prettier 忽略 |
| [eslint.config.js](assets/eslint.config.js) | ESLint Flat Config |
| [.lintstagedrc.json](assets/.lintstagedrc.json) | lint-staged 配置 |
| [.editorconfig](assets/.editorconfig) | 编辑器配置 |
| [commitlint.config.js](assets/commitlint.config.js) | commitlint 配置（可选） |

> 根据框架类型调整 ESLint 配置，详见 [frameworks.md](references/frameworks.md)

### 第四步：初始化 Husky

```bash
npx husky init
echo "npx lint-staged" > .husky/pre-commit
```

### 第五步：验证配置

```bash
npm run lint
npm run format:check
git add . && git commit -m "chore: 初始化项目配置"
```

## 框架特定配置

详见 [frameworks.md](references/frameworks.md)

- React + Vite
- Vue 3
- Next.js
- Node.js
- 纯 TypeScript

## 常见问题

| 问题 | 解决方案 |
|------|----------|
| ESLint 与 Prettier 冲突 | 安装 `eslint-config-prettier` 并放在 extends 最后 |
| Husky hooks 不执行 | 确认 `.husky/` 目录存在且有执行权限 |
| TypeScript 路径别名报错 | 在 ESLint 配置中添加 `settings: { 'import/resolver': { typescript: {} } }` |
| 旧版 ESLint 配置迁移 | 使用 `npx @eslint/migrate-config .eslintrc.json` |

## 输出清单

```
.
├── .editorconfig
├── .prettierrc
├── .prettierignore
├── .husky/
│   └── pre-commit
├── eslint.config.js
├── commitlint.config.js   # 可选
└── package.json           # 含 scripts 和 lint-staged
```
