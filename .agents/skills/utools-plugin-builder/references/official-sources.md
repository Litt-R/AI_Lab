# Official uTools Sources

Use these links as routing hints, not as a frozen copy of the documentation. Open only the pages needed for the current task and check the page as it exists now.

| Need | Official page |
| --- | --- |
| Documentation root and navigation | https://www.u-tools.cn/docs/ |
| First-time project workflow and development entry | https://www.u-tools.cn/docs/getting-started/overview.html |
| Runtime layers, BrowserView model, environment | https://www.u-tools.cn/docs/development/plugin-architecture.html |
| `plugin.json`, features, commands, tools | https://www.u-tools.cn/docs/development/plugin-json.html |
| Preload, CommonJS, Node and Electron access | https://www.u-tools.cn/docs/development/preload.html |
| Synced data, local data, temporary files, user files | https://www.u-tools.cn/docs/development/storage.html |
| Additional BrowserWindow behavior | https://www.u-tools.cn/docs/development/custom-window.html |
| MCP server and plugin tools | https://www.u-tools.cn/docs/development/mcp.html |
| Plugin lifecycle and host events | https://www.u-tools.cn/docs/api-reference/events.html |
| System, path, OS, and utility APIs | https://www.u-tools.cn/docs/api-reference/system.html |
| Main window, dialogs, and window APIs | https://www.u-tools.cn/docs/api-reference/window.html |
| Database API and document model | https://www.u-tools.cn/docs/api-reference/db.html |
| AI model and registered-tool APIs | https://www.u-tools.cn/docs/api-reference/ai.html |
| Vendor's own development skill | https://www.u-tools.cn/docs/ai/plugin-dev-skill.html |
| Official GitHub organization | https://github.com/uTools-Labs |
| Vendor development skill, useful as an instruction-writing reference; it contains documentation but no sample project | https://github.com/uTools-Labs/utools-plugin-dev-skill |
| Official development examples and entry-point templates | https://github.com/uTools-Labs/utools-tutorials |
| Official uTools API type definitions | https://github.com/uTools-Labs/utools-api-types |
| Official documentation source repository | https://github.com/uTools-Labs/utools-docs |

## Retrieval Rules

- Use live official pages for exact API names, casing, parameter order, return values, defaults, required configuration, and lifecycle semantics.
- Search the documentation root when the relevant topic is not listed here.
- Prefer the narrowest page or section that answers the current contract question.
- A packaged reference snapshot may help when the live site is unavailable. Record that it is a fallback and identify its version or retrieval date before relying on release-specific facts.
- If live documentation and a packaged snapshot disagree, investigate the current runtime or current type definitions; report the discrepancy instead of silently choosing one.
- Keep implementation and architecture choices independent. Official documents define the host contract, while the user's requirements and the project's evidence guide product decisions.
- Use the official GitHub organization for current repository structure, examples, release history, changelogs, and source inspection.
- Treat the official documentation site as the primary contract for published uTools APIs. A GitHub issue, discussion, community reply, or draft branch is context unless the project presents it as released behavior.
- Read only the repositories and files relevant to the current feature. Do not clone or import an entire organization or vendor skill when opening the specific source is sufficient.
- Use the tutorials repository to inspect concrete manifest layouts and feature-entry patterns; adapt the example to the current task instead of copying it wholesale.
- Use the API type definitions as a fast secondary check for names and shapes, then confirm published behavior on the official documentation site or runtime.
