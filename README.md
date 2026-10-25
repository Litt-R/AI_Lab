# AI_Lab

[中文](README.md) | [English](README.en.md)

探索多种 AI Agent 与 CLI 工具的个人试验项目，当前包含 Claude Code 和 Codex。主要探索 Skill、Agent 配置、工作流与协作方式，各工具的配置和技能可以在同一项目中并存。

## 内容

```
.claude/
└── skills/                     Claude Code 的可复用工作流指令
.agents/
└── skills/                     Codex 的可复用工作流指令
notes/                          探索笔记与经验记录
```

## Skills

`.claude/skills/` 与 `.agents/skills/` 分别维护 Claude Code 和 Codex 的 Skill。两侧共同维护以下六个 Skill；其中 `utools-plugin-builder` 按需查阅当前官方文档，辅助开发 uTools 插件：

| Skill | 用途 |
| --- | --- |
| `load-mem` | 开始工作时恢复项目记忆与上下文 |
| `save-mem` | 保存可复用的决策与项目知识 |
| `init-mem` | 初始化项目记忆系统；已有系统则检查补齐 |
| `task-handoff` | 任务暂停与恢复，支持 save / resume |
| `project-structure` | 诊断项目结构问题并提出重组方案 |
| `utools-plugin-builder` | 查官方文档并开发、修改或排查 uTools 插件 |

## 笔记

`notes/` 记录探索过程中积累的、可跨项目复用的经验。

## 许可

[MIT](LICENSE)
