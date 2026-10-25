# AI_Lab

[中文](README.md) | [English](README.en.md)

A personal playground for exploring multiple AI agents and CLI tools, currently including Claude Code and Codex. It covers skills, agent configuration, workflows, and collaboration, with each tool's configuration and skills coexisting in the same project.

## Contents

```
.claude/
└── skills/                     Claude Code workflow instructions
.agents/
└── skills/                     Codex workflow instructions
notes/                          Exploration notes and lessons learned
```

## Skills

`.claude/skills/` and `.agents/skills/` maintain skills for Claude Code and Codex separately. Both provide these six skills; `utools-plugin-builder` consults current official documentation when developing uTools plugins:

| Skill | Purpose |
| --- | --- |
| `load-mem` | Restore project memory and context at the start of work |
| `save-mem` | Persist reusable decisions and project knowledge |
| `init-mem` | Initialize project memory, or inspect and fill gaps in an existing system |
| `task-handoff` | Pause and resume tasks, with save / resume modes |
| `project-structure` | Diagnose structural problems and propose reorganizations |
| `utools-plugin-builder` | Develop, modify, or troubleshoot uTools plugins using current official documentation |

## Notes

`notes/` records experience gained during exploration that applies across projects.

## License

[MIT](LICENSE)
