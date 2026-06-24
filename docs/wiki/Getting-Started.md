# Getting Started

This guide walks you through installing the Handoff extension and seeing it in action for the first time.

## Prerequisites

- **VS Code 1.90** or later
- A project containing a `.handoff/` directory (created by [handoff-mcp](https://github.com/alphaelements/handoff-mcp))

## Install the Extension

Search for **"Handoff"** in the VS Code Extensions panel, or run:

```
ext install alphaelements.handoff-vscode
```

## Quick Start

1. Install [handoff-mcp](https://github.com/alphaelements/handoff-mcp) and initialize a project with `handoff_init`.
2. Install this extension from the Marketplace.
3. Open the folder containing `.handoff/` in VS Code.

The Task Explorer appears automatically in the sidebar, and the Dashboard is available from the Command Palette.

## Try the Demo

If you want to explore the extension before setting up handoff-mcp, clone the public repository:

```bash
git clone https://github.com/alphaelements/handoff-vscode.git
code handoff-vscode
```

The repo includes a `.handoff/` directory with a realistic sample project — 42 tasks across multiple milestones, 6 AI sessions, effort budgets, assignee calendars, and more. The extension picks it up automatically when you open the folder.

## First Things to Try

**Open the Dashboard** — Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on macOS), type `Handoff: Open Dashboard`, and press Enter. You will see task counts, a Kanban board, effort budget, and a recent activity feed.

**Browse the Task Explorer** — Look at the sidebar. The Handoff icon opens a tree view of all tasks grouped by status, with priority badges, labels, and stale-day indicators.

**Check the Gantt Chart** — Open it from the Command Palette with `Handoff: Open Gantt Chart`. The interactive timeline shows scheduled tasks, milestones, and dependency arrows.

**View Metrics** — Open the Metrics panel (`Handoff: Open Metrics`) to see completion rates, velocity trends, and effort budget allocation.

## Next Steps

- [Task Explorer](Task-Explorer) — Learn about filtering, sorting, and context menu actions
- [Dashboard](Dashboard) — Understand each panel in the project overview
- [Configuration](Configuration) — Customize settings and locale
