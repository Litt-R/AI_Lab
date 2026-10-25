---
name: save-mem
description: Use when the user asks to save durable project or collaboration knowledge, or when a handoff workflow reviews the current work for reusable decisions and the project defines memory storage rules.
---

# Save Memory

Record durable, reusable knowledge in the project's established Claude memory system. Read `CLAUDE.md` for its conventions. With the default layout, follow `.claude/specs/memory-and-handoff.sdoc` when present and update `.claude/memory/MEMORY.md` whenever a memory entry changes. Follow explicitly documented project paths when they differ; do not write to another agent's memory unless sharing is explicitly configured.

Write human-facing memory notes and index entries in the project's documented language; if none is specified, use the user's language, defaulting to Simplified Chinese for this user. Preserve code identifiers, paths, and necessary technical terms. Keep project-local Skill instructions in English.

`save-mem` is the promotion step from a candidate to durable project memory. A candidate may come directly from the user, from verified current work, or from a task-handoff checkpoint.

1. Check the project's current memory instructions, index, and existing notes before writing. Update an existing note when it already covers the fact.
2. Apply the promotion gate. Save only knowledge that is verified, reusable beyond the immediate next action, attributable to the active project, and safe to retain. During an active task, promote a fact early only when it is already confirmed and likely to affect later work; otherwise leave it as a handoff candidate.
3. Do not promote routine progress, temporary next actions, unresolved proposals, secrets, unrelated-project material, or facts that still depend on an unfinished implementation. Those remain in the task checkpoint or are reported as ineligible.
4. At task completion, promote candidates only after the relevant behavior and evidence have stabilized. If an older candidate has not been verified against the current project, keep it pending or correct it before writing.
5. Choose the appropriate memory layer and granularity according to project rules. One memory note should carry one useful fact. Prefer correcting the canonical existing note over appending a conflicting duplicate.
6. Preserve the source, scope, dates, conditions, and any remaining uncertainty. Keep explicit decisions distinct from proposals and historical context.
7. Update the relevant index or links so the note can be found. Do not invent storage locations or layer rules if none are documented.
8. Report what was promoted, updated, left pending, or rejected, and where it was stored. If no durable knowledge qualifies, or the memory system is not configured, say so and do not create an empty memory entry or initialize a new system implicitly.
