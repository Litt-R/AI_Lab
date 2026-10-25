---
name: init-mem
description: Initialize a project's memory system, or inspect and fill gaps in an existing one when asked. Preserve existing knowledge and project conventions; identify any migration or major reorganization before changing it.
---

# Initialize Memory

Use this workflow when the user asks to initialize or repair a project's memory system. If no system exists, establish its conventions, specifications, and index. If one already exists, inspect it and fill only missing or inconsistent parts; a repeat invocation must preserve existing knowledge and must not reset or duplicate the system. When initialization requires migration or major reorganization, describe the affected material and proceed only within the user's agreed scope. This workflow concerns the active project, not moving memory between projects.

Write human-facing specifications, memory notes, and indexes in the active project's documented language. If none is specified, use the user's language, defaulting to Simplified Chinese for this user. Preserve code identifiers, filenames, and technical terms where appropriate. Keep project-local Skill instructions in English.

1. Inspect the target project's `AGENTS.md`, existing memory files, indexes, handoffs, and relevant documentation before proposing changes. Keep other agents' configurations and memory intact; migration into Codex does not authorize replacing or removing their systems.
2. Follow current project-specific memory conventions. If none exist, use this default layout, adapting it only with the user's agreement:
- `.agents/specs/` for current normative project rules and stable decisions;
- `.agents/memory/` for project-local reusable context, with `MEMORY.md` as its index;
- `.agents/handoffs/` for per-task session checkpoints.
3. If the `strictdoc` CLI is available in the active environment (`strictdoc --version` succeeds), use StrictDoc for normative project management content: author and maintain it as `.sdoc` in the documented Codex specs directory (default `.agents/specs/`). Carefully migrate confirmed current normative rules and stable decisions from other formats; do not blindly convert informational documents, Skill instructions, or task progress. Keep Magic Context notes and task handoffs in Markdown.
4. When StrictDoc is available and this workflow creates or changes `.sdoc` files, validate and generate HTML by exporting only the documented Codex specs directory from the project root. Use the project's documented output directory; the default example is `strictdoc export .agents/specs --output-dir output/specs`. Do not use the whole repository as input or overwrite another agent's export. Report the actual generated HTML entry point, normally `<output-dir>/html/index.html`. If export fails, report the failure and do not claim validation succeeded.
5. If StrictDoc is unavailable and the project has not already adopted it, do not create unvalidated `.sdoc` content or claim StrictDoc compliance. Preserve the existing format and tell the user what installation or follow-up is needed. Existing project conventions take precedence.
6. Use lowercase kebab-case for descriptive filenames; use `MEMORY.md` for the memory index. Avoid creating empty directories or documents for layers the project will not use.
7. Distinguish current policy, durable decisions, reusable background, and task-specific progress. Respect the project's stated authority and conflict rules.
8. Ask focused questions when an unresolved storage, scope, or conflict decision would materially affect the design. Do not ask about facts discoverable from existing project files.
9. Create or update only the agreed index, memory notes, and specifications. Preserve useful existing material; do not wholesale rewrite, delete, or move original files without explicit agreement.
10. Check links, paths, indexes, and available validators. Report what changed, what was not migrated, and any remaining decisions.

Do not use this workflow for routine memory updates or task handoffs; use `save-mem`, `load-mem`, or `task-handoff` as appropriate.
