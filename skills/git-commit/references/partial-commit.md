# 部分提交

当用户明确指定只提交部分文件时（如"只提交 stylelint 配置"、"先提交配置部分"）：

## 识别用户意图

- "只提交配置" → 只提交配置文件
- "先提交 stylelint" → 只提交 stylelint 相关文件
- "暂不提交 unit4" → 排除 unit4 相关文件

## 执行

只添加相关文件并提交：

```bash
# 示例: 只提交 stylelint 配置
git add .stylelintrc.json .vscode/settings.json package.json pnpm-lock.yaml
git commit -m "chore: 集成 Stylelint"
```

## 提交后告知

- 哪些文件已提交
- 哪些文件未提交（仍在工作区）
- 询问是否继续提交其他改动
