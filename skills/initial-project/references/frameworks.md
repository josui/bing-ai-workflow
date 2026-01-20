# 框架特定配置

## React + Vite

额外安装：

```bash
pnpm add -D vite-plugin-eslint2
```

ESLint 配置已包含 React 插件，无需额外配置。

## Vue 3

额外安装：

```bash
pnpm add -D eslint-plugin-vue @vue/eslint-config-typescript
```

ESLint 配置示例：

```javascript
import js from '@eslint/js'
import tseslint from 'typescript-eslint'
import vue from 'eslint-plugin-vue'

export default tseslint.config(
  js.configs.recommended,
  ...tseslint.configs.recommended,
  ...vue.configs['flat/recommended'],
  {
    rules: {
      'vue/multi-word-component-names': 'off',
    },
  }
)
```

## Next.js

使用内置 ESLint 配置：

```bash
pnpm add -D @next/eslint-plugin-next
```

ESLint 配置示例：

```javascript
import js from '@eslint/js'
import tseslint from 'typescript-eslint'
import next from '@next/eslint-plugin-next'

export default tseslint.config(
  js.configs.recommended,
  ...tseslint.configs.recommended,
  {
    plugins: {
      '@next/next': next,
    },
    rules: {
      ...next.configs.recommended.rules,
    },
  }
)
```

## Node.js

额外安装：

```bash
pnpm add -D eslint-plugin-n
```

ESLint 配置示例：

```javascript
import js from '@eslint/js'
import tseslint from 'typescript-eslint'
import n from 'eslint-plugin-n'

export default tseslint.config(
  js.configs.recommended,
  ...tseslint.configs.recommended,
  n.configs['flat/recommended'],
  {
    rules: {
      'n/no-missing-import': 'off', // TypeScript 已处理
    },
  }
)
```

## 纯 TypeScript

无需额外框架插件，使用基础配置即可：

```javascript
import js from '@eslint/js'
import tseslint from 'typescript-eslint'

export default tseslint.config(
  js.configs.recommended,
  ...tseslint.configs.recommended,
  {
    rules: {
      '@typescript-eslint/no-unused-vars': 'error',
      '@typescript-eslint/no-explicit-any': 'error',
    },
  }
)
```
