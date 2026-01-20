# SKILL.md 规范

## Front Matter（YAML 头部）

```yaml
---
name: skill-name # 必需，小写+连字符
description: 描述文本 # 必需，用于技能匹配
license: MIT # 可选
metadata: # 可选
  author: your-name
  version: '1.0'
---
```

**命名规则：**

- 最多 64 字符
- 仅小写字母、数字、连字符
- 不能以连字符开头或结尾

✅ `react-patterns`, `code-review`
❌ `React-Patterns`, `-react`, `react--patterns`

## 正文最佳实践

| 建议          | 说明                     |
| ------------- | ------------------------ |
| < 5000 tokens | 主文件保持简洁           |
| 明确触发条件  | description 决定何时加载 |
| 提供代码示例  | 帮助 AI 理解预期         |
| 拆分大型内容  | 详细文档放 `references/` |

## 可选目录

```
my-skill/
├── SKILL.md           # 必需 - 主指令
├── scripts/           # 可选 - 可执行脚本
│   └── analyze.py
├── references/        # 可选 - 参考文档（按需加载）
│   └── advanced.md
└── assets/            # 可选 - 模板、配置文件
    └── template.json
```

**引用方式（在 SKILL.md 中）：**

```markdown
详见 [高级指南](references/advanced.md)

运行脚本：`python scripts/analyze.py`
```
