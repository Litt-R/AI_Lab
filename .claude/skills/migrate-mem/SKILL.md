---
name: migrate-mem
description: Use when the user asks to establish, repair, or materially reorganize a project's memory system. Audit existing instructions and memories first; preserve project conventions and avoid assuming one universal architecture.
---

# Migrate Memory

Use this workflow only when the user asks to establish, repair, or materially reorganize a project's memory system. This concerns that project internally; it is not a mechanism for moving memory between projects.

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
7. Distinguish current policy, durable decisions, reusable background, and task-specific progress. Respect the project's stated authority and conflict rules.
8. Ask focused questions when an unresolved storage, scope, or conflict decision would materially affect the design. Do not ask about facts discoverable from existing project files.
9. Create or update only the agreed index, memory notes, and specifications. Preserve useful existing material; do not wholesale rewrite, delete, or move original files without explicit agreement.
10. Check links, paths, indexes, and available validators. Report what changed, what was not migrated, and any remaining decisions.

Do not use this workflow for routine memory updates or task handoffs; use `save-mem`, `load-mem`, or `task-handoff` as appropriate.
