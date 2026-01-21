# AI Workflow Skills

通用 AI 编码助手技能集合。

> 项目介绍、技能列表、安装方式详见 [README.md](../README.md)

## 文档获取

查询外部文档时优先使用 MCP 工具：

1. **[ref.tools](https://ref.tools/)** - 查询包版本、API 文档、兼容性信息
2. **context7 MCP** - 获取最新官方文档和配置示例

备选：Web Search 调查不确定的内容。

## 开发指南

### 添加新技能

1. 在 `skills/` 下创建新目录
2. 按照 [skill-format.md](doc/skill-format.md) 规范编写 `SKILL.md`
3. 更新 `README.md` 技能列表

### 目录结构

```
skills/<skill-name>/
├── SKILL.md           # 必需 - 主指令
├── README.md          # 技能说明
├── references/        # 可选 - 参考文档
└── assets/            # 可选 - 模板文件
```

### Git 提交

始终使用 `git-commit` skill 提交更新。
