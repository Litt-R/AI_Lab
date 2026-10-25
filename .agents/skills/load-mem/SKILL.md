---
name: load-mem
description: Use at the start of a work session or when resuming an ongoing task if the project has a documented memory system. Restore relevant context and verify remembered facts against current instructions and code.
---

# Load Memory

Restore useful project context without treating old notes as current instructions by default. Read `AGENTS.md` to find the project's documented memory conventions. For a Codex memory system using this skill's default layout, read `.agents/specs/memory-and-handoff.sdoc` first when present, then use `.agents/memory/MEMORY.md` to find relevant single-fact notes. Follow explicitly documented project paths when they differ.

When summarizing project memory for a human, use the project's documented language; if unspecified, use the user's language, defaulting to Simplified Chinese for this user. Keep project-local Skill instructions in English.

1. Look for the project's documented memory locations and index; inspect the applicable `AGENTS.md` guidance first. Another agent's memory is not Codex's memory unless the project explicitly documents sharing.
2. Load only memories relevant to the current task rather than dumping the entire archive.
3. Separate current durable decisions, project facts, user preferences, and historical notes. Prefer an explicitly current normative document over conflicting historical memory.
4. Verify remembered file paths, symbols, settings, and commands still exist before relying on them. Use current code and configuration as evidence.
5. Note stale or contradictory context briefly when it affects the task. Do not silently convert guesses into project rules.
6. Treat memory candidates stored in a checkpoint as pending evidence, not durable memory. Surface only candidates relevant to the resumed task and never promote or rewrite them during loading; promotion belongs to `save-mem` after verification.
7. Do not read a separate built-in or global memory store unless project instructions document it or the user explicitly requests it. If the project has no documented memory system, state that memory loading was skipped. Do not guess memory paths or initialize the system automatically; ask or use `init-mem` only when the user requests establishing or repairing memory.
