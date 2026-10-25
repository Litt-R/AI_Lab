---
name: utools-plugin-builder
description: Build, modify, debug, and extend uTools plugin apps, including greenfield prototypes and existing projects. Use for plugin.json, BrowserView and preload boundaries, lifecycle, storage, custom windows, native integrations, AI or MCP tools, scheduling, and uTools-specific troubleshooting.
---

# uTools Plugin Builder

Ship a working plugin while keeping engineering control. Let official documentation define the host contract; use the project, tests, and sound application design to decide how to fulfill the request.

This skill supports both new plugins and incremental development. Creating a small runnable plugin, choosing a frontend, or replacing an unsuitable technical approach is allowed when the user's goal calls for it.

## Working Model

A uTools plugin normally combines these layers:

- **Web UI:** HTML/CSS/JavaScript and an optional frontend framework. It renders the interface and often calls `window.utools` directly.
- **Preload bridge:** CommonJS code with access to Node.js, Electron renderer capabilities, and uTools APIs. Expose a small, named API to the UI instead of leaking privileged objects.
- **uTools host:** Runs the plugin UI in a managed `BrowserView`, supplies lifecycle and platform APIs, and can host additional `BrowserWindow` instances created by the plugin.
- **Manifest:** `plugin.json` identifies the main HTML entry, logo, optional preload, feature triggers, and optional AI tools.

Treat this as a starting model, not a rigid template. Adapt it to the existing project and the user's runtime constraints.

## Evidence and Judgment

Use evidence in this order for host behavior:

1. The current project's actual configuration, code, tests, and observed uTools runtime.
2. Current official uTools API and configuration documentation.
3. A reproducible experiment in uTools Developer Tools or an explicitly available test environment.
4. The local reference snapshot or other secondary explanation.
5. A clearly labeled inference.

Official docs are authoritative for names, signatures, required fields, defaults, and supported host behavior. They do not dictate product scope, code style, framework choice, or whether the task should be implemented. Do not copy vendor workflow restrictions into the application.

When documentation is incomplete, investigate with the available runtime, type definitions, examples, or a focused probe. State what remains unverified. Never invent a host API or present browser-only behavior as proof of uTools behavior.

For exact APIs, start with [the official source map](references/official-sources.md), open the relevant live uTools documentation page, and verify version-specific behavior before relying on it. A packaged or local snapshot is an offline fallback, not proof that a fact is current.

## First Inspect the Project

Before editing, identify:

- `plugin.json`: `main`, `logo`, `preload`, `features`, `tools`, and build assumptions.
- Entry HTML and frontend framework, assets, routes, and state management.
- Preload bridge and every global interface exposed to the renderer.
- Feature codes, command triggers, payload shapes, and the code that routes them.
- Build scripts and package manager; verify whether source files or generated files are loaded by the plugin.
- Storage types, migrations, cleanup, and any sync behavior.
- Existing tests, type checks, linting, and uTools Developer Tools workflow.

Prefer current project patterns when they are sound. Refactor only when the requested goal or a concrete defect justifies the cost.

## Choose the Smallest Coherent Design

Map each requirement to the right uTools mechanism:

| Need | Preferred mechanism |
| --- | --- |
| Searchable command or matched text, files, image, or window | `features[].cmds` |
| UI in the standard plugin surface | Manifest `main` loaded in the managed view |
| Node, filesystem, process, native modules, or Electron APIs | Preload bridge |
| Independently managed window | uTools custom browser-window API |
| Cross-device structured user data | uTools database |
| Persistent device-local data | Plugin local data path |
| Disposable working files | Plugin temporary directory |
| User-visible exports | User-selected destination or system downloads path |
| AI-callable capability | Manifest `tools` plus runtime tool registration |
| Background or repeated work | uTools scheduling lifecycle |
| Embedded media/image processing | Built-in FFmpeg or Sharp capability after verification |
| Browser automation | uTools uBrowser after verifying the workflow |

Use an ordinary web or Node solution when the host does not need to provide the capability. Use a uTools API when it gives the correct lifecycle, permissions, storage, or integration.

### Greenfield path

For a new plugin, establish only the files needed for the smallest useful flow:

1. A valid `plugin.json` with a relative HTML main, logo, and at least one feature.
2. A minimal UI that can enter the requested feature.
3. A preload bridge only if the UI needs privileged local capabilities.
4. A repeatable build only when source transformation or dependencies require it.
5. A real uTools runtime test for features that cannot be proven statically.

Do not inflate a prototype with framework boilerplate, a library, or a generalized architecture that the requested feature does not need.

## Lifecycle and Data Rules

- Register each plugin-level listener once in an appropriate long-lived preload or entry context.
- Use ready-time initialization for async work that must finish before the plugin becomes usable.
- Route `onPluginEnter` by `code`; handle `type`, `payload`, and `from` according to the actual feature trigger.
- Handle `onPluginOut` carefully. `isKill` distinguishes process shutdown from hiding to the background.
- Put interrupted work, retries, and resume state in storage deliberately rather than assuming the renderer stays alive.
- Separate synced structured user data from device-local caches, logs, indexes, binaries, and temporary artifacts.
- Design schema versions, migrations, cleanup, and failure recovery before adding persistent data.
- Keep user exports in locations the user can discover and manage.

## Security and Bridge Design

Expose intention-level methods, not privileged primitives. Validate paths, commands, URLs, and untrusted payloads at the preload boundary. Avoid giving the renderer raw `fs`, `child_process`, broad IPC, or arbitrary command execution when a narrow operation is enough.

Set explicit success and failure results. Do not swallow errors, fabricate completed operations, or use background providers to conceal failed local work.

## Implementation

Make the smallest coherent change that satisfies the requested behavior. Preserve unrelated functionality and dependencies. Keep feature declarations, handlers, UI routes, IPC channels, tool schemas, and storage together by responsibility.

When changing an API integration:

1. Verify the exact host API and invocation context.
2. Check asynchronous return behavior and error cases.
3. Update every matching manifest or runtime declaration.
4. Run the narrowest useful static or build check.
5. Exercise the affected flow in uTools when possible.

Do not claim a UI interaction, plugin entry, window, native bridge, scheduling trigger, or data sync has been verified unless it was actually exercised.

## Validation

Use checks proportional to the change:

- Parse `plugin.json` and ensure referenced files exist in the packaged output.
- Confirm unique feature codes, useful commands, and trigger payload handling.
- Check preload CommonJS loading and dependency packaging.
- Check every `window.utools` and bridge call against the current contract.
- Test success, empty, invalid, permission, cancellation, and failure paths.
- Verify manifest tools and registered handlers agree in name, schema, and result shape.
- Run existing type checks, tests, and builds.
- Test at least one real entry-to-result path in uTools Developer Tools for UI or lifecycle changes.
- Distinguish static validation, build success, and runtime verification in the report.

## Completion

Report the user-visible behavior, important files, how the flow works, verification performed, and any blocker or unverified behavior. If a platform capability is unavailable, say what was observed and offer the nearest sound alternative. Keep output concise unless the user asks for implementation detail.