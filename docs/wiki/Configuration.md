# Configuration

The Handoff extension is configured through two mechanisms: **VS Code settings** (for extension behavior) and **config.toml** (for project-level data like effort budgets, milestones, and calendars).

## VS Code Settings

These settings are available under `handoff.*` in VS Code Settings (Ctrl+, / Cmd+,):

### General

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `handoff.autoRefresh` | boolean | `true` | Watch the `.handoff/` directory for changes and refresh automatically |
| `handoff.autoRefreshInterval` | number | `30000` | Auto-refresh interval in milliseconds |
| `handoff.refreshDebounceMs` | number | `300` | Debounce delay for file watcher refresh (ms) |
| `handoff.locale` | string | `"auto"` | UI language: `"en"` or `"ja"`. `"auto"` follows the VS Code display language |
| `handoff.defaultView` | string | `"dashboard"` | Default panel view when opening Handoff (`dashboard`, `gantt`, `metrics`, `team`) |
| `handoff.overworkLimitPercent` | number | `150` | Warn when workload exceeds this percentage of capacity |

### Scanning

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `handoff.scan.depth` | number | `5` | Maximum directory depth when scanning for `.handoff/` directories |
| `handoff.scan.excludePatterns` | string[] | `["node_modules", ".git", "dist", "out", "build", ".next", ".venv", "target"]` | Directory patterns to skip during scan |

### Status Bar

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `handoff.statusBar.enabled` | boolean | `true` | Show status bar items |
| `handoff.statusBar.showHours` | boolean | `true` | Show effort hours in the status bar |
| `handoff.statusBar.showBranch` | boolean | `true` | Show current Git branch in the status bar |
| `handoff.statusBar.showSession` | boolean | `true` | Show active session indicator in the status bar |

### Task Explorer

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `handoff.taskExplorer.groupByStatus` | boolean | `true` | Group tasks by status in the tree view |
| `handoff.taskExplorer.showDoneTasks` | boolean | `true` | Show completed tasks in the explorer |
| `handoff.taskExplorer.showSkippedTasks` | boolean | `false` | Show skipped tasks in the explorer |
| `handoff.taskExplorer.sortBy` | string | `"order"` | Default sort mode: `order`, `priority`, `updated`, `created`, or `due` |

### Gantt Chart

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `handoff.gantt.defaultScale` | string | `"day"` | Gantt chart time scale: `"day"` or `"week"` |

### Time Tracker

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `handoff.timeTracker.enabled` | boolean | `true` | Enable or disable the time tracker entirely |
| `handoff.timeTracker.autoStart` | boolean | `true` | Automatically start the timer when a task is set to `in_progress` |
| `handoff.timeTracker.idleTimeoutMinutes` | number | `3` | Minutes of inactivity before the timer pauses automatically |
| `handoff.timeTracker.showInStatusBar` | boolean | `true` | Show the running timer in the status bar |
| `handoff.timeTracker.minLogMinutes` | number | `1` | Minimum minutes to log — shorter durations are discarded on stop |

### Setting the Language

The extension supports English and Japanese. To set the language explicitly:

```json
{
  "handoff.locale": "en"
}
```

Leave it empty (the default) to follow whatever language VS Code is set to.

## Project Configuration (config.toml)

Each project's `.handoff/config.toml` file controls project-level settings. This file is created and managed by [handoff-mcp](https://github.com/alphaelements/handoff-mcp), but you can edit it manually.

### Basic Fields

```toml
project_name = "My Project"
version = "0.4"
default_branch = "main"
```

### Effort Budget

Set the total hours budgeted for the project. The extension tracks how much has been allocated, spent, and remains.

```toml
[effort_budget]
total_hours = 200
```

See [Dashboard](Dashboard.md) and [Metrics](Metrics.md) for how budget data is displayed.

### Calendar

Define working hours, days off, and per-weekday hour overrides. The Gantt chart and workload calculations use this data.

```toml
[calendar]
work_start_hour = 9
work_end_hour = 18
closed_weekdays = ["sat", "sun"]
closed_dates = ["2026-12-25", "2026-01-01"]
open_dates = ["2026-12-28"]       # Override a normally closed day
schedule_mode = "manual"           # "manual" or "auto"
overwork_limit_percent = 150       # Warn when workload exceeds this %
```

Override hours for specific weekdays:

```toml
[calendar.day_hours]
wed = 3
fri = 4
```

### Assignees

Define team members with individual schedules and display settings. Assignees appear in the Gantt chart and workload views.

```toml
[assignees.alice]
display_name = "Alice Chen"
color = "#0097A7"
work_hours_per_day = 8
closed_weekdays = ["mon", "tue"]
closed_dates = ["2026-06-23"]
open_dates = ["2026-06-21"]

[assignees.bob]
display_name = "Bob Martinez"
color = "#E05490"
work_hours_per_day = 6
day_hours = { fri = 4 }
```

Each assignee supports:

| Field | Type | Description |
|-------|------|-------------|
| `display_name` | string | Name shown in the UI |
| `color` | string | Hex color for Gantt bars and charts |
| `work_hours_per_day` | number | Default hours per working day |
| `closed_weekdays` | string[] | Days the person does not work |
| `closed_dates` | string[] | Specific dates off (YYYY-MM-DD) |
| `open_dates` | string[] | Override closed days as working |
| `day_hours` | object | Per-weekday hour overrides (e.g. `{ fri = 4 }`) |

### Milestones

Define project milestones with dates and colors. These appear in the Gantt chart as diamond markers and in the Dashboard and Metrics as grouping categories.

```toml
[milestones."v1.0"]
date = "2026-07-15"
color = "#FF6B35"
description = "Initial public release"

[milestones."v1.1"]
date = "2026-08-30"
color = "#0097A7"
description = "Performance improvements"
```

### Gantt View Defaults

Set the default view state for the Gantt chart. Users can change these interactively; the values here are the initial state.

```toml
[gantt_view]
zoom = "day"                    # "day" or "week"
sort = "start"                  # Sort tasks by start date
mode = "compare"                # "plan", "actual", or "compare"
group_by_milestone = false
group_by_assignee = false
filter_assignee = ""            # Filter to a specific assignee key
show_workload = true
workload_view = "total"         # "total" or "per-assignee"
```

## File Structure

For reference, a fully configured `.handoff/` directory looks like this:

```
.handoff/
  config.toml
  tasks/
    t1-feature-name/
      _task.in_progress.json
    t2-another-task/
      _task.done.json
  sessions/
    2026-06-15T0900-planning.open.json
  referrals/
    20260610-auth-service.open.json
```

## Related

- [Getting Started](Getting-Started.md) — Initial setup
- [Gantt Chart](Gantt-Chart.md) — Uses calendar and milestone data
- [Dashboard](Dashboard.md) — Uses effort budget data
- [FAQ](FAQ.md) — Common configuration questions
