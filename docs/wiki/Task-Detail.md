# Task Detail

The Task Detail panel displays the full information for a single task and lets you edit its status, schedule, dependencies, and done criteria without leaving VS Code.

## Opening the Panel

- **Task Explorer**: Click any task in the sidebar [tree view](Task-Explorer) to open its detail panel.
- **Kanban Board**: Click a card on the [Dashboard](Dashboard) Kanban board.
- **Command Palette**: Run `Handoff: Open Task` and select a task from the quick-pick list.

The panel opens as a tab alongside your editor.

## Done Criteria

Each task can have a checklist of acceptance criteria. Items appear as interactive checkboxes — click to toggle, or use the command:

- **Command**: `Handoff: Toggle Done Criterion`

A progress indicator (e.g. `3/5`) shows how many criteria are checked. Changes write back to the task's `_task.*.json` file immediately.

## Status

A dropdown at the top of the panel shows the current task status. Select a new value to change it:

| Status | Description |
|--------|-------------|
| todo | Not yet started |
| in_progress | Actively being worked on |
| review | Awaiting review |
| done | Completed |
| blocked | Cannot proceed (dependencies or external factors) |
| skipped | Intentionally dropped |

- **Command**: `Handoff: Set Status`

Changing status to `in_progress` can automatically start the [Time Tracker](Time-Tracker) if `handoff.timeTracker.autoStart` is enabled. Changing away from `in_progress` stops and logs the elapsed time.

## Priority

A dropdown to set the task's priority level:

| Priority | Badge |
|----------|-------|
| high | P1 (orange) |
| medium | P2 (blue) |
| low | P3 (gray) |

- **Command**: `Handoff: Set Priority`

Priority affects sort order in the [Task Explorer](Task-Explorer) and visual emphasis in the [Gantt Chart](Gantt-Chart).

## Labels

Labels appear as colored tags below the task title (e.g. `backend`, `auth`, `frontend`). Labels are set by [handoff-mcp](https://github.com/alphaelements/handoff-mcp) and displayed here for reference. You can filter by label in the Task Explorer.

## Notes

The notes section shows the task's description or any freeform text. Markdown formatting is supported. Notes provide context about the task's purpose, technical approach, or constraints.

## Schedule

The schedule section displays and lets you edit the task's timeline and effort tracking.

| Field | Description |
|-------|-------------|
| Start Date | When work is planned to begin (`schedule.start_date`) |
| Due Date | Target completion date (`schedule.due_date`) |
| Estimate Hours | Planned effort in hours (`schedule.estimate_hours`) |
| Actual Hours | Hours spent so far (`schedule.actual_hours`) |
| Milestone | The milestone this task belongs to (e.g. `v1.0`) |

- **Command**: `Handoff: Edit Schedule` — opens a quick-pick flow to update start date, due date, estimate, or milestone.

A progress bar shows actual hours relative to the estimate. When actual exceeds the estimate, the bar turns red to flag an overrun.

Dates edited here are also reflected in the [Gantt Chart](Gantt-Chart), and vice versa — dragging a bar in the Gantt view updates the schedule shown in Task Detail.

## Dependencies

The dependencies section lists tasks that must be completed before this one can proceed.

- **Command**: `Handoff: Add Dependency` — select a task to add as a dependency.
- **Command**: `Handoff: Remove Dependency` — remove an existing dependency link.

When a task has unresolved dependencies (the depended-on task is not `done`), the detail panel highlights which dependencies are blocking progress. This is also reflected in the Task Explorer, where blocked tasks show a warning indicator.

Dependencies appear as arrows in the [Gantt Chart](Gantt-Chart) connecting the depended-on task to the dependent one.

## Display Order

Each task has an `order` field that controls its position among siblings in the Task Explorer. Lower values appear first.

- **Command**: `Handoff: Set Display Order` — set the numeric order value for the task.

The order is typically set by the AI agent via handoff-mcp to reflect a recommended work sequence. You can override it manually when needed.

## Time Tracking

When the [Time Tracker](Time-Tracker) is running for this task, the detail panel shows:

- A live elapsed-time counter
- Controls to pause, stop, or cancel the timer

Stopped time is accumulated into `schedule.actual_hours`. See the [Time Tracker](Time-Tracker) page for details on auto-start, idle detection, and persistence.

## Timestamps

The bottom of the panel displays read-only timestamps:

| Timestamp | Description |
|-----------|-------------|
| Created | When the task was first created (`created_at`) |
| Updated | When any field was last modified (`updated_at`) |
| Completed | When the task was marked `done` (`completed_at`) — only shown for completed tasks |
