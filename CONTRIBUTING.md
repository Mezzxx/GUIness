# Contributing to GUIness

Thanks for your interest in contributing. This guide covers the ground rules and workflow for getting changes merged.

## Before You Start

GUIness is a **single-file application** by design. That constraint is load-bearing — it enables the portability, zero-dependency, and offline-first properties that define the project. Contributions that introduce external dependencies, build steps, or multi-file architectures will not be accepted.

## Ground Rules

1. **One file.** All JS, CSS, and HTML live in `guiness.html`. No splitting, no imports, no bundlers.
2. **No external dependencies.** No CDN links, no npm packages, no fetched scripts. Everything is self-contained.
3. **Match existing style.** Read the code around your change and follow the same patterns — naming, indentation, comment style. Don't reformat adjacent code.
4. **Surgical changes.** Touch only what your change requires. Don't refactor nearby code, rename unrelated variables, or "improve" things outside your scope.
5. **No speculative features.** If it wasn't discussed in an issue first, open one before writing code.

## How to Contribute

### Reporting Bugs

Open an issue with:

- What you expected to happen
- What actually happened
- Steps to reproduce (browser, OS, and any relevant console errors)
- A screenshot or screen recording if it's a visual bug

### Suggesting Features

Open an issue describing:

- The problem you're trying to solve (not just the solution you want)
- How you currently work around it, if applicable
- Whether you're willing to implement it yourself

### Submitting Code

1. **Fork** the repo and create a branch from `main`
2. **Open an issue first** if the change is non-trivial (anything beyond typo fixes)
3. **Make your change** in a focused, minimal commit
4. **Test in at least two browsers** (Chrome + Firefox recommended)
5. **Open a pull request** with a clear description of what changed and why

### Pull Request Expectations

- One logical change per PR. Don't bundle unrelated fixes.
- The PR description should explain the *why*, not just the *what*.
- If your change modifies runtime behavior, describe how you tested it.
- If your change touches the canvas, node rendering, or edge drawing, include a screenshot or GIF showing before/after.
- Keep the diff small. Large PRs take longer to review and are more likely to be asked to split up.

## Code Conventions

- **Variables:** camelCase for locals, UPPER_SNAKE for constants in `CONFIG`
- **Functions:** camelCase, verb-first (`buildNode`, `renderEdges`, `callAI`)
- **Colors:** OKLCH values via the `COLORS` map or `THEME_PRESETS`
- **State:** modify `skills[]`, `pipelines[]`, `activePipelineId`, `selNode`/`selNodes` through existing patterns — don't introduce new global state without discussion
- **DOM:** use existing helper patterns for element creation; don't introduce jQuery-style abstractions
- **Security:** any user input that touches innerHTML must go through sanitization. Use the `safeStore` pattern for stored values.

## What Gets Accepted

- Bug fixes with clear reproduction steps
- Performance improvements with before/after measurements
- UX improvements that don't change the interaction model without discussion
- Documentation improvements
- Accessibility improvements

## What Gets Declined

- Multi-file refactors or build system additions
- External dependency introductions (npm, CDN, etc.)
- Large-scope rewrites without prior discussion
- Style-only changes (reformatting, renaming) with no functional improvement
- Features that duplicate existing functionality

## Questions?

Open an issue. Conversations happen in the open.
