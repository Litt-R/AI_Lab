---
name: init-mem
description: Initialize a project's memory system, or inspect and fill gaps in an existing one when asked. Preserve existing knowledge and project conventions; identify any migration or major reorganization before changing it.
---

# Initialize Memory

Use this workflow when the user asks to initialize or repair a project's memory system. If no system exists, establish its conventions, specifications, and index. If one already exists, inspect it and fill only missing or inconsistent parts; a repeat invocation must preserve existing knowledge and must not reset or duplicate the system. When initialization requires migration or major reorganization, describe the affected material and proceed only within the user's agreed scope. This workflow concerns the active project, not moving memory between projects.

Once a memory system is healthy, do not use this workflow as a routine task-start step. Start or resume tasks through `task-handoff` and load relevant memory through `load-mem`. Use `init-mem` for initial setup, repair, or explicit maintenance.

Write human-facing specifications, memory notes, and indexes in the active project's documented language. If none is specified, use the user's language, defaulting to Simplified Chinese for this user. Preserve code identifiers, filenames, and technical terms where appropriate. Keep project-local Skill instructions in English.

1. Inspect the target project's instructions, existing memory files, indexes, handoffs, and relevant documentation before proposing changes.
2. Follow current project-specific memory conventions. If none exist, use this default layout, adapting it only with the user's agreement:
- `.claude/specs/` for current normative project rules and stable decisions;
- `.claude/memory/` for project-local reusable context, with `MEMORY.md` as its index;
- `.claude/handoffs/` for per-task session checkpoints.
3. If the `strictdoc` CLI is available in the active environment (`strictdoc --version` succeeds), use StrictDoc for normative project management content: author and maintain it as `.sdoc` in `.claude/specs/`. Carefully migrate confirmed current normative rules and stable decisions from other formats; do not blindly convert informational documents, Skill instructions, or task progress. Keep Magic Context notes and task handoffs in Markdown.
4. When StrictDoc is available and this workflow creates or changes `.sdoc` files, validate and generate HTML by exporting only `.claude/specs/` from the project root to the consistent path `output/specs/`, for example: `strictdoc export .claude/specs --output-dir output/specs`. Do not use the whole repository as input. Report the generated HTML entry point, normally `output/specs/html/index.html`. If export fails, report the failure and do not claim validation succeeded.
5. If StrictDoc is unavailable and the project has not already adopted it, do not create unvalidated `.sdoc` content or claim StrictDoc compliance. Preserve the existing format and tell the user what installation or follow-up is needed. Existing project conventions take precedence.
6. Use lowercase kebab-case for descriptive filenames; use `MEMORY.md` for the memory index. Avoid creating empty directories or documents for layers the project will not use.
7. Keep the lifecycle explicit: task checkpoints may contain pending memory candidates; `save-mem` promotes verified candidates into durable notes; `load-mem` reads them without writing. Respect the project's stated authority and conflict rules.
8. Ask focused questions when an unresolved storage, scope, or conflict decision would materially affect the design. Do not ask about facts discoverable from existing project files.
9. Identify any separate built-in or global memory feature documented for the active agent. Do not inspect undocumented stores or another agent's memory by default. When such a feature is present, ask whether the user wants current-project material audited for import, and whether project memory should remain the authoritative source. Before changing a global or automatic-memory setting, ask separately and explain the effect; never disable it silently.
10. If the user approves an import, present the eligibility boundary and avoid bulk-merging global data. Keep only durable, verified facts clearly attributable to the active project; exclude secrets, task progress, unrelated projects, and stale guesses. Preserve provenance and update the project index. Leave ambiguous or sensitive candidates for user review instead of importing them automatically.
11. If this invocation is explicit maintenance, audit duplicate, stale, conflicting, or unindexed material and consolidate it into canonical notes. Do not delete a memory solely because of age; verify it against current instructions, code, or explicit user decisions first. Keep historical context when it explains a current decision.
12. Create or update only the agreed index, memory notes, and specifications. Preserve useful existing material; do not wholesale rewrite, delete, or move original files without explicit agreement.
13. Check links, paths, indexes, and available validators. Report what changed, what was not migrated, pending candidates, the automatic-memory decision if applicable, and any remaining decisions.

Do not use this workflow for routine memory updates or task handoffs; use `save-mem`, `load-mem`, or `task-handoff` as appropriate.
