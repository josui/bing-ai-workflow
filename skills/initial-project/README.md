# initial-project

项目初始化技能，一站式配置开发工具。

## 功能

- 配置 Prettier（代码格式化）
- 配置 ESLint（代码质量检查）
- 配置 Husky（Git hooks 管理）
- 配置 lint-staged（暂存文件检查）
- 可选：commitlint、Stylelint、EditorConfig

## 触发词

- `/initial-project`
- `初始化项目`
- `配置开发环境`

## 安装

```bash
npx add-skill josui/bing-ai-workflow -s initial-project
```

## 支持的框架

- React + Vite
- Vue 3
- Next.js
- Node.js
- 纯 TypeScript

## 输出文件

```
.
├── .editorconfig
├── .prettierrc
├── .prettierignore
├── .husky/
│   └── pre-commit
├── eslint.config.js
├── commitlint.config.js  # 可选
└── package.json          # 含 scripts 和 lint-staged
```
