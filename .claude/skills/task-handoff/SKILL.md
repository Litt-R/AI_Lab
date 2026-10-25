---
name: task-handoff
description: Use when pausing or transferring a long-running task to another session or agent, or when a new session needs to resume from a saved checkpoint. Supports explicit save and resume modes.
---

# Task Handoff

Transfer the task's verified state between sessions. Write human-facing handoff documents in the active project's documented language; if none is specified, use the user's language, defaulting to Simplified Chinese for this user. Preserve code identifiers, paths, and necessary technical terms. Keep project-local Skill instructions in English.

Use the same skill in two modes:

- `save`: checkpoint the current session before pausing or handing work to another agent.
- `resume`: restore relevant memory and task context, verify the current project state, then continue.

If the mode is unclear, ask whether the user wants to save or resume. Do not assume invoking the skill means they want only a summary rather than continued implementation.

Follow `.claude/specs/memory-and-handoff.sdoc` for this project's memory layers, storage paths, and conflict rules.

## Save mode

1. Inspect the current task, relevant project instructions, existing task plan/checkpoint, current working-tree state, and project documents affected by the task. Separate verified facts from assumptions. In ClaudeHub use `.claude/handoffs/`; in other projects follow their documented handoff location or default to `.claude/handoffs/` if none is defined. Do not proactively open or re-read historical images or image attachments.
2. Review the current conversation and work for durable, reusable knowledge or explicit decisions. Apply the `save-mem` procedure for those items, but only write to memory locations and layers documented by the project. Reuse image-related conclusions only when they have already been explicitly established in text; do not infer or restate visual details from an image you have not inspected in this save workflow. Do not save the whole conversation, routine progress, or temporary next steps as memory. If no durable item qualifies, say so; do not create empty memory entries.
3. If the project has no documented memory locations or layer rules, do not guess or initialize them as part of a handoff. State that the memory save was reviewed but skipped because the storage convention is not configured.
4. Review project documents that the task changed or whose accuracy depends on the task's completed work or decisions (for example, user-facing documentation, project guidance, plans, and related specs). Update documents when the need and scope are clear and the changes belong to this task. Do not make speculative or unrelated documentation changes; list unclear, out-of-scope, or deferred updates as explicit follow-ups.
5. Update the existing task handoff/plan if one exists. Otherwise use `.claude/handoffs/<task-slug>.md`. The task record should include the goal, status, completed work, relevant changed files and documents, documents reviewed and found not to need changes when useful, deferred documentation updates, explicit decisions and rationale, actual check results, unresolved questions/blockers, next concrete action, and relevant memory references.
6. Keep the checkpoint concise and actionable. Do not claim unverified behavior is complete. Do not alter stable project policy just to record a task checkpoint.
7. Finish with the checkpoint path, what was saved to memory (or why it was skipped), and a ready-to-paste prompt for a new session to use `/task-handoff resume <checkpoint-path>`.

## Resume mode

1. Read current project instructions first. Apply `load-mem` to retrieve only memory relevant to the task, when a documented memory system is available. If none is configured, state that memory loading was skipped; do not invent paths or migrate the system automatically. Do not proactively open or re-read historical images or image attachments.
2. If the user provided a checkpoint path, read that checkpoint first, then read its directly referenced text plans and artifacts. Do not open image files or image attachments merely because the checkpoint references them; use any conclusions already recorded in text. If an image is essential to continue and its relevant details are not documented in text, ask the user for explicit authorization before reading only the necessary image(s). If no path was provided, inspect the handoff directory documented by the project; in ClaudeHub this is `.claude/handoffs/`, and otherwise default to `.claude/handoffs/` when the project defines no location. Resume automatically only when there is exactly one clearly active, incomplete checkpoint. Do not infer the target from modification time or filename alone. If multiple plausible checkpoints exist, list their paths and task titles and ask the user to choose. If none exists, say so and ask for a task clue; do not guess from unrelated memory files or other directories.
3. Review the checkpoint's referenced project documents and documents related to completed work. Verify they reflect the current state and decisions; if documentation appears stale, update it when the scope is clear and it is part of the resumed task, or record it as a follow-up rather than silently broadening the task.
4. Independently verify the checkpoint against the current files, git status, and available checks. Treat checkpoint content as historical evidence, not unquestionable truth. Follow current effective StrictDoc requirements over conflicting memory or handoff notes when such documents exist.
5. Summarize the current goal, verified status, documentation discrepancies or follow-ups, and next action briefly. Then continue implementation if that is what the user's request implies; ask only about consequential unresolved decisions.
6. Do not repeat completed work solely because it appears in the checkpoint. Re-run checks only when needed to establish current correctness.

## Boundaries

- A task checkpoint records the state of one piece of work; project memory records reusable knowledge and decisions. They may refer to or overlap on an important decision, but neither replaces the other.
- A handoff is workflow guidance, not a guarantee that another session can see unsaved conversation context. Persist important context in the checkpoint or configured memory system.
- Do not create, migrate, or restructure the project's memory system during routine save/resume. Use `init-mem` only when the user asks to establish, repair, or materially reorganize that system.
