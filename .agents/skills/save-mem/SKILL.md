---
name: save-mem
description: Use when the user asks to save durable project or collaboration knowledge, or when a handoff workflow reviews the current work for reusable decisions and the project defines memory storage rules.
---

# Save Memory

Record durable, reusable knowledge in the project's established Codex memory system. Read `AGENTS.md` for its conventions. With the default layout, follow `.agents/specs/memory-and-handoff.sdoc` when present and update `.agents/memory/MEMORY.md` whenever a memory entry changes. Follow explicitly documented project paths when they differ; do not write to another agent's memory unless sharing is explicitly configured.

Write human-facing memory notes and index entries in the project's documented language; if none is specified, use the user's language, defaulting to Simplified Chinese for this user. Preserve code identifiers, paths, and necessary technical terms. Keep project-local Skill instructions in English.

1. Check the project's current memory instructions, index, and existing notes before writing. Update an existing note when it already covers the fact.
2. Save decisions, project knowledge, or collaboration preferences likely to matter beyond this task. Do not save the whole conversation, routine progress, or temporary next actions; those belong to a task checkpoint.
3. Choose the appropriate memory layer and granularity according to project rules. Related knowledge may be recorded in more than one layer when the rules allow it. Do not force an artificial separation.
4. Preserve uncertainty, scope, dates, and conditions. Keep explicit decisions distinct from proposals and historical context.
5. Update the relevant index or links so the note can be found. Do not invent storage locations or layer rules if none are documented.
6. Report what was recorded and where. If no durable knowledge qualifies, or the memory system is not configured, say so and do not create an empty memory entry or initialize a new system implicitly.
