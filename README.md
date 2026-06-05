# GUIness

A self-contained, single-file visual skill pipeline editor for building and chaining AI prompt workflows. No external dependencies, no build step, no server required.

## What It Does

**[▶ Open the app](https://guiness.zeen-media.com/)**  ·  **[Documentation](https://guiness.zeen-media.com/docs/)**

GUIness is a node-based pipeline editor (think Blender Geometry Nodes, but for AI skills) that lets you visually compose, connect, and execute chains of AI prompts. Each node represents a skill — a reusable prompt template with typed inputs and outputs — and pipelines wire them together into multi-step workflows.

Everything lives in one HTML file (~745 KB, ~7,800 lines of JS). Open it in a browser and start building.

## Features

- **Visual node editor** with drag-and-drop wiring, minimap, and canvas navigation
- **8 built-in primitive skills** (Starter Gems) ready to use out of the box
- **AI-powered execution** via `callAI` / `callAIStreaming` with chain-of-thought pipeline runs
- **Skills library** with JSON save/load, shift-click multi-select, and import/export
- **Gem export** tab for generating Gemini Custom Instructions from pipelines
- **AI-generated `internalGraph`** for complex skill decomposition
- **Vault** for secure API key storage with `safeStore` XSS-hardened wrapper
- **Gist sync** for cloud backup and sharing
- **Autosave** with local storage persistence
- **Social posting** integration
- **File cards** with drag-and-drop support
- **OKLCH color theming** with preset themes
- **Collapsible panels** and responsive layout
- **Cycle detection** via Kahn's algorithm to prevent infinite loops
- **Zero dependencies** — fully portable, runs offline

## Getting Started

1. **Use it now** — open the live app at **[guiness.zeen-media.com](https://guiness.zeen-media.com/)**; nothing to install
2. **Or run it yourself** — download `index.html` from this repo (or grab a tagged build from [Releases](https://github.com/Mezzxx/GUIness/releases)) and open it in any modern browser
3. That's it

No `npm install`. No `docker compose`. No environment variables. Just a browser.

### Quick Tour

- **Pipeline tab** — create, edit, delete, and run pipelines
- **Library tab** — browse, import, and manage reusable skills
- **Inspector panel** — configure the selected node's parameters
- **Canvas** — drag nodes, draw edges between ports, pan and zoom
- **Minimap** — birds-eye navigation for large pipelines

## Usage

### Building a Pipeline

1. Open the **Library** and drag a skill onto the canvas (or use the add menu)
2. Connect output ports to input ports by clicking and dragging between them
3. Configure each node's parameters in the **Inspector**
4. Hit **Run** to execute the chain

### Creating Custom Skills

Skills are JSON objects with a name, description, input/output port definitions, and a prompt template. You can create them in the Library tab or write them by hand and import via JSON.

### Vault

Store your API keys in the Vault. Keys are persisted in local storage and accessed through the `safeStore` wrapper, which sanitizes values to prevent XSS injection.

### Gist Sync

Link a GitHub Gist to back up your pipelines and skills to the cloud. Useful for sharing setups across machines.

## Architecture

Everything is in one file by design. The key pieces:

| Section | What It Does |
|---|---|
| `CONFIG` | Magic numbers, defaults, constants |
| `THEME_PRESETS` / `COLORS` | OKLCH color system and theme definitions |
| `skills[]` | The 8 built-in primitive skills |
| `pipelines[]` / `activePipelineId` | Pipeline state and active selection |
| `canvasStack` | Canvas rendering and navigation state |
| `selNode` / `selNodes` | Current node selection (single and multi) |
| `buildNode` | Creates a node DOM element from a skill definition |
| `renderEdges` | Draws SVG connections between ports |
| `renderInspector` | Builds the inspector panel for the selected node |
| `renderLib` | Renders the skills library panel |
| `callAI` / `callAIStreaming` | AI execution (single and streaming) |
| `runChain` | Executes a full pipeline via topological sort |
| `renderMdResponse` | Renders markdown AI responses |

## Portability

The single-file, zero-dependency constraint is intentional. GUIness is designed to be:

- **Emailable** — send the file to a collaborator, they open it, done
- **Archivable** — one file to back up, no `node_modules` rot
- **Offline-capable** — even the fonts are inlined, so the only network calls are the AI requests you trigger (and optional Gist sync)
- **Private by design** — there's no server in the path, so your API keys and prompts never leave your browser except to reach the model provider you chose
- **Forkable** — no build toolchain to understand before making changes

## License

MIT

## Author

[mezzn](https://github.com/Mezzxx) — [Zeen Media](https://zeen-media.com)
