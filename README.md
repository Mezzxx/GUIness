# GUIness

A self-contained, single-file visual skill pipeline editor for building and chaining AI prompt workflows. No external dependencies, no build step, no server required.

## What It Does

GUIness is a node-based pipeline editor (think Blender Geometry Nodes, but for AI skills) that lets you visually compose, connect, and execute chains of AI prompts. Each node represents a skill — a reusable prompt template with typed inputs and outputs — and pipelines wire them together into multi-step workflows.

Everything lives in one HTML file (~780KB, ~13,000 lines of JS). Open it in a browser and start building. Checkout the [docs](https://guiness.zeen-media.com/docs/) for a more in-depth breakdown.

## Features

- **Visual node editor** with drag-and-drop wiring, minimap, lasso selection, alignment guides, and canvas navigation
- **8 built-in primitive skills** (Starter Gems) ready to use out of the box
- **Multi-URL FETCH** and **multi-file FILE** primitives for batch data ingestion
- **AI-powered execution** via `callAI` / `callAIStreaming` with chain-of-thought pipeline runs
- **Live chain execution** — nodes pulse amber while running, flip to green ✓ / red ✕ on complete/error, with a bottom-center HUD showing progress and a Stop button
- **Pre-flight validation** — orphan and missing-input detection before a run, with amber ⚠ flags on problem nodes and a Run Anyway / Cancel gate
- **Bulk Fetch** (Shift+F) — fetch all selected FETCH nodes in one operation
- **Skills library** with JSON save/load, shift-click multi-select, and import/export
- **Skill import diffing** — imported skills show NEW / UPDATE chips with behavior-field comparison against existing library entries
- **Portable workspace** — export/import all pipelines + skills as a single `.gwsp` file for cross-device portability
- **Gem export** tab for generating Gemini Custom Instructions from pipelines
- **AI-generated `internalGraph`** for complex skill decomposition
- **Vault** for secure API key storage with `safeStore` XSS-hardened wrapper and idle auto-relock (15-minute default)
- **Safe expression parser** — Router JS-mode conditions use a recursive-descent parser instead of `eval`/`new Function`, closing the XSS surface
- **Gist sync** for cloud backup and sharing
- **Autosave** with localStorage persistence and optional file-system backup
- **Customizable keyboard shortcuts** — remap any binding via the ⌨ Keys overlay
- **Quick-add search** (Q or double-click canvas) for fast node placement
- **Context menu** (right-click node) — Set as Start Node, Save as Skill, Merge, Copy/Paste, Duplicate, Delete
- **Social posting** integration (Bluesky, LinkedIn, Twitter/X, Instagram)
- **File cards** with drag-and-drop support
- **OKLCH color theming** with five preset themes and light/dark toggle
- **Collapsible panels** and responsive layout with resizable panel widths
- **Cycle detection** via Kahn's algorithm to prevent infinite loops
- **Zero dependencies** — fully portable, runs offline

## Getting Started

1. You can run it from [GUIness](https://guiness.zeen-media.com/), or download/clone this repo.
2. Open index.html in any modern browser
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
| `runChain` / `runNodeWithState` | Executes a full pipeline via topological sort with live canvas visualization |
| `preflight` | Pure pre-run validation (orphans, missing inputs) |
| `safeEvalCondition` | Safe recursive-descent expression parser for Router conditions |
| `renderMdResponse` | Renders markdown AI responses |
| `exportWorkspace` / `importWorkspace` | Portable `.gwsp` workspace save/restore |

## Portability

The single-file, zero-dependency constraint is intentional. GUIness is designed to be:

- **Emailable** — send the file to a collaborator, they open it, done
- **Archivable** — one file to back up, no `node_modules` rot
- **Offline-capable** — works without internet (except AI calls and Gist sync)
- **Forkable** — no build toolchain to understand before making changes
- **Workspace-portable** — export all pipelines + skills as a single `.gwsp` file and import on another machine

## License

MIT

## Author

[mezzn](https://github.com/Mezzxx) — [Zeen Media](https://zeen-media.com)
