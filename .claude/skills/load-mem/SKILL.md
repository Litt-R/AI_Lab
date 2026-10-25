---
name: load-mem
description: Use at the start of a work session or when resuming an ongoing task if the project has a documented memory system. Restore relevant context and verify remembered facts against current instructions and code.
---

# Load Memory

Restore useful project context without treating old notes as current instructions by default. In ClaudeHub, read `.claude/specs/memory-and-handoff.sdoc` first, then use `.claude/memory/MEMORY.md` to find relevant single-fact notes. For other projects, follow their own instructions and do not assume this project's paths apply.

When summarizing project memory for a human, use the project's documented language; if unspecified, use the user's language, defaulting to Simplified Chinese for this user. Keep project-local Skill instructions in English.

1. Look for the project's documented memory locations and index; inspect the applicable `CLAUDE.md` or `AGENTS.md` guidance first.
2. Load only memories relevant to the current task rather than dumping the entire archive.
3. Separate current durable decisions, project facts, user preferences, and historical notes. Prefer an explicitly current normative document over conflicting historical memory.
4. Verify remembered file paths, symbols, settings, and commands still exist before relying on them. Use current code and configuration as evidence.
5. Note stale or contradictory context briefly when it affects the task. Do not silently convert guesses into project rules.
6. If the project has no documented memory system, state that memory loading was skipped. Do not guess memory paths or initialize the system automatically; ask or use `init-mem` only when the user requests establishing or repairing memory.
