---
name: project-structure
description: Use when a growing project has become hard to navigate, feels cluttered, or needs a structural assessment or reorganization. Diagnose from a developer and user-understanding perspective, propose a project-specific architecture, then carry out the approved scope, including large-scale restructuring when appropriate.
---

# Project Structure

Help the user keep a growing project understandable, navigable, and maintainable. Optimize for clear concepts, cohesive boundaries, discoverable entry points, and an architecture that can evolve. Do not force a generic directory template or treat project size itself as a defect.

## Workflow

1. **Establish the baseline.** Read project guidance, identify purpose, primary users and entry points, languages/frameworks, build/test/release flows, and current architecture. Inventory the tree and inspect relevant code/configuration references to understand responsibilities and dependencies.
2. **Diagnose real friction.** Look for folders that mix unrelated concepts, responsibilities fragmented across too many places, duplicate or obsolete areas, unclear ownership, tangled dependencies, misleading names, hard-to-find workflows, and structures that make onboarding or ordinary changes difficult. Explain concrete evidence and user/developer impact; distinguish facts from hypotheses.
3. **Design for this project.** Propose a coherent target structure based on domain concepts, cohesion, dependency direction, team/user workflows, and likely evolution. The entire structure may change: it can be appropriate to merge scattered folders, split overloaded folders, create new organizing boundaries, or relocate modules and documentation. Consider broad changes when they materially improve comprehensibility; do not optimize for cosmetic symmetry or minimize the scope at the expense of a good architecture.
4. **Protect version history first.** Determine the repository root, active branch, and `git status`; identify tracked, untracked, ignored, and already-modified files. Preserve all user changes. Never run destructive Git commands such as `reset --hard`, `clean`, or an unrequested checkout; never overwrite or discard work. For a large cross-cutting change, recommend a dedicated feature branch and a clean or clearly understood baseline, but do not create/switch branches or commit unless requested. If the project is not a Git repository, or overlapping uncommitted changes make safe execution unclear, explain the risk and ask how to establish a recoverable baseline before editing.
5. **Write the proposal before restructuring.** Save a new Simplified Chinese Markdown assessment at `.claude/structure-assessments/YYYY-MM-DD-project-structure.md`, using the project's documented location if it explicitly specifies another. If the name already exists, add a descriptive suffix; never overwrite an earlier assessment. Include:
- project purpose and assessed scope;
- current-tree observations and evidence;
- user-facing and developer-facing friction;
- proposed target tree and responsibility of each major area;
- folder/module merges, splits, moves, renames, and any file removals;
- reference/configuration/build/test impact and migration sequence;
- Git baseline/branch/status and safeguards;
- validation plan, risks, and status `待用户确认`.
6. **Get approval for the plan.** Present the proposal and wait for the user's explicit confirmation before changing the project structure. The user may approve a broad redesign; do not reduce it to incremental tidying merely because it is large. Approval covers the operations and removals explicitly listed in the report. If important new scope appears, update the proposal and ask again.
7. **Execute the approved restructuring.** Apply coherent batches of moves, merges, splits, and necessary code/config/reference updates. Use Git-aware moves where practical so history remains recognizable. Do not commit unless asked. If unexpected work overlaps with user edits, stop and protect those edits; do not stash, revert, or overwrite them automatically.
8. **Verify and close the loop.** Inspect the resulting tree, `git status`, and diff (including rename detection); check for stale paths/imports, run relevant focused tests/builds or other project checks, and report unverified behavior. Update the same assessment with what was actually changed, validation results, deviations, and remaining work. Never claim a check passed unless it did.

## Use and boundaries

- Invoke when the user asks to assess or reorganize structure. Relevant natural-language requests may trigger this skill.
- If substantial growth, accumulated structural friction, or navigation/maintenance problems emerge during other work, suggest an assessment and wait for agreement before starting it.
- This skill does not monitor projects in the background or run automatically after every change.
- The assessment is a human-readable decision and execution record, not a normative specification; keep it in Markdown and use Simplified Chinese by default. Preserve identifiers, paths, and necessary technical terms.
- If evidence shows no meaningful structural problem, say so and avoid inventing a restructuring exercise.
