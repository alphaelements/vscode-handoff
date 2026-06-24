# FAQ

## Nothing shows up in the sidebar

Make sure the workspace you opened contains a `.handoff/` directory at its root. The extension looks for `.handoff/tasks/` to populate the Task Explorer.

If you're trying the extension for the first time, clone this repository and open it in VS Code. It includes demo data in its `.handoff/` directory.

To create `.handoff/` for your own project, use [handoff-mcp](https://github.com/alphaelements/handoff-mcp) and run `handoff_init`.

## How do I create tasks?

Tasks are created through [handoff-mcp](https://github.com/alphaelements/handoff-mcp), the MCP server that manages the `.handoff/` data. The VS Code extension is a viewer and lightweight editor — it reads and displays task data, but task creation happens through the MCP server (typically during AI coding sessions).

## Can I edit tasks from the extension?

Some operations write back to `.handoff/` automatically:

- **Status changes** via the Kanban board (drag-and-drop) or context menu
- **Time tracking** accumulates into `schedule.actual_hours`
- **Done criteria** checkboxes toggle in the task detail panel
- **Gantt chart** drag-to-reschedule updates `start_date` and `due_date`

For full task editing (title, description, labels, dependencies, etc.), use handoff-mcp.

## Does it work with multiple workspaces?

Yes. When you open a multi-root workspace in VS Code, the extension reads `.handoff/` from each workspace folder and merges the tasks into a single view. Each project's tasks are grouped under the project name.

## How do I change the language?

Set the `handoff.locale` setting to `"en"` (English) or `"ja"` (Japanese):

```json
{
  "handoff.locale": "ja"
}
```

If left empty (the default), the extension follows the VS Code display language.

## The Gantt chart dates look off by one day

The Gantt chart uses local time for all date calculations and display. If dates appear shifted, check that your system timezone is set correctly. This can happen when running VS Code in a container or remote environment where the timezone differs from what you expect.

## How does the effort budget work?

1. Set `total_hours` in `.handoff/config.toml` under `[effort_budget]`
2. The extension calculates:
   - **Allocated** — Sum of all tasks' `estimate_hours`
   - **Actual** — Sum of all tasks' `actual_hours`
   - **Pool** — Unallocated hours remaining in the budget
3. The Dashboard and Metrics panels show budget health with color-coded status: Healthy (green), Low (yellow), Critical (red), or Overbudget

When a task finishes under estimate, the savings return to the pool. When a task goes over, the overage is deducted. This happens automatically based on the task data.

## Where is the data stored?

All data lives in the `.handoff/` directory as plain JSON and TOML files:

```
.handoff/
  config.toml          # Project settings, budget, milestones
  tasks/               # One directory per task
    t1-name/
      _task.done.json  # Status is encoded in the filename
  sessions/            # AI session history
  referrals/           # Cross-project referrals
```

These files are designed to be version-controlled. You can commit `.handoff/` to your repository to share project state with your team.

## Can I use this without handoff-mcp?

Technically, yes. If you create a `.handoff/` directory with properly formatted task JSON files, the extension will read and display them. However, the intended workflow is to use handoff-mcp to manage the data and the extension to visualize it.

## How do I report a bug?

Open an issue on the [GitHub repository](https://github.com/alphaelements/handoff-vscode/issues/new/choose). Bug report and feature request templates are available.

## Related

- [Getting Started](Getting-Started.md) — Setup instructions
- [Configuration](Configuration.md) — Full settings reference
