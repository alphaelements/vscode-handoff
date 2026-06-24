# Task Explorer

The Task Explorer is a tree view in the VS Code sidebar that gives you an at-a-glance overview of every task in your project. Tasks are grouped by status and decorated with icons, badges, and inline metrics so you can quickly find what needs attention.

## Opening the Task Explorer

The Task Explorer appears automatically when you open a folder containing a `.handoff/` directory. You can also show it manually:

- **Command Palette**: `Handoff: Focus on Handoff View`
- **Activity Bar**: Click the Handoff icon in the sidebar

## Status Groups

Tasks are organized into collapsible groups, ordered by urgency:

| Status | Icon | Color | Description |
|--------|------|-------|-------------|
| Blocked | Slashed circle | Red | Waiting on a dependency or external input |
| In Progress | Half-filled circle | Yellow | Actively being worked on |
| Review | Dot-center circle | Purple | Work complete, awaiting review |
| Todo | Empty circle | Blue | Not yet started |
| Done | Filled circle with check | Green | Completed (collapsed by default) |
| Skipped | Circle with X | Gray | Intentionally skipped (collapsed by default) |

The `done` and `skipped` groups are collapsed by default to keep the view focused on active work.

## Task Row Details

Each task row displays several pieces of information at a glance:

- **Status icon** — colored SVG glyph matching the task's current status
- **Priority badge** — `P0` (critical, red), `P1` (high, orange), `P2` (medium, blue), or `P3` (low, gray)
- **Task title** — the task name
- **NEXT flag** — a green label highlighting the recommended next task to work on (based on the `order` field set by AI or manually)
- **Labels** — tag pills such as `backend`, `auth`, `frontend`
- **Effort hours** — inline display of estimated vs. actual hours (e.g. `4/8h`)
- **Stale indicator** — shows how long a task has been in its current status:
  - 4–7 days: yellow warning
  - 7+ days: red warning
- **Overdue warning** — a triangle icon appears when the task is past its due date
- **Dependency warning** — shown when the task depends on another task that is not yet complete

## Filtering

Use the filter bar at the top of the Task Explorer to narrow the task list. You can filter by:

- **Text search** — type in the "Filter tasks..." input to match task titles
- **Status** — show only tasks in a specific status (e.g. just `in_progress` and `review`)
- **Label** — filter by one or more labels
- **Priority** — filter by priority level
- **Milestone** — show only tasks assigned to a specific milestone

Filters can be combined. The active filter state is shown in the filter bar.

## Sorting

Click the sort pill (e.g. `order`) in the filter bar to cycle through sort modes:

| Sort Mode | Description |
|-----------|-------------|
| Order | AI-recommended priority order (default) |
| Priority | Critical first, then high, medium, low |
| Due Date | Earliest deadline first |
| Updated | Most recently changed first |
| Created | Newest tasks first |

## Interactions

- **Click** a task to open its [Task Detail](Dashboard.md) panel in the editor area
- **Right-click** a task to open the context menu with quick actions:
  - Change status (e.g. move from `todo` to `in_progress`)
  - Change priority
  - Open task detail
- **Collapse/expand** status groups by clicking the group header
- **Refresh** the task list using the refresh icon in the view header or `Handoff: Refresh Tasks` from the Command Palette

## Auto-Refresh

When `handoff.autoRefresh` is enabled (the default), the Task Explorer watches the `.handoff/` directory for changes and updates automatically. The refresh interval is configurable via `handoff.autoRefreshInterval` (default: 30 seconds).

See [Configuration](Configuration.md) for all available settings.
