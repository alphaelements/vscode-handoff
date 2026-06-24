# Team Panel

The Team panel provides a dedicated view for managing project members and monitoring team capacity. It consolidates member management, task assignment, and workload visibility into a single tab.

## Opening the Team Panel

- **Command Palette**: `Handoff: Open Team`
- **Tab Bar**: Click the **Team** tab in the Handoff panel (next to Dashboard, Gantt, and Metrics)

## Capacity Summary

The top row shows four summary cards for the team as a whole:

| Card | Description |
|------|-------------|
| Members | Number of registered team members |
| Daily Capacity | Combined work hours per day across all members |
| Total Tasks | Total tasks in the project |
| Unassigned | Tasks with no assignee |

## Member Cards

Below the summary, each team member is shown as an expandable card.

### Collapsed View (default)

Each card displays:

- **Color dot and name** -- the member's assigned color and display name
- **Hours per day** -- daily work capacity (e.g. `8h/d`)
- **Completion rate** -- percentage of assigned tasks completed
- **Task breakdown** -- counts for active, done, blocked, and overdue tasks
- **Status distribution bar** -- a compact bar showing the proportion of todo, in progress, review, done, and blocked tasks
- **Effort progress bar** -- actual hours worked vs. allocated estimate hours, with remaining hours shown

### Expanded View

Click a member card to expand it and see:

- **Assigned Tasks** -- a list of the member's active tasks (excludes done and skipped). Each row shows the task status icon, title, and an unassign button to remove the member from that task.
- **Quick Assign** -- a list of up to five unassigned tasks that can be assigned to this member with one click. If more than five unassigned tasks exist, a "+N more" indicator appears.

### Unassigned Section

An "Unassigned" group at the bottom of the card list collects all tasks that have no assignee. This section does not show a Quick Assign area, but tasks listed here can be assigned from any member's expanded card.

## Managing Members

The **Manage Members** section at the bottom of the panel lists all registered members and provides controls for adding, editing, and removing them.

### Member List

Each row shows the member's color, name, daily hours, and assigned task count, along with edit and delete buttons.

### Adding a Member

Click the **+** button to open the add form:

- **Name** -- the member's display name
- **Color** -- choose from eight preset colors or pick a custom color
- **Hours/day** -- daily work capacity (default: 8, range: 1--24, step: 0.5)

Press Enter or click **Add** to save. Press Escape or click **Cancel** to dismiss the form. The member key is generated automatically from the name (lowercased, non-alphanumeric characters replaced with underscores).

### Editing a Member

Click the edit button on any member row to open the same form pre-filled with current values. Click **Update** to save changes.

### Removing a Member

Click the delete button to remove a member. If the member has assigned tasks, a confirmation dialog appears showing how many tasks are affected. Tasks previously assigned to the removed member become unassigned.

## Where Members are Defined

Members are stored in `config.toml` under `[assignees.<key>]` sections. Each member supports the following fields:

| Field | Description |
|-------|-------------|
| `display_name` | Name shown in the UI |
| `color` | Hex color code (e.g. `"#0097A7"`) |
| `work_hours_per_day` | Daily capacity in hours |
| `closed_weekdays` | Days off (e.g. `["sun", "sat"]`) |
| `closed_dates` | Specific dates off (e.g. `["2026-07-04"]`) |
| `open_dates` | Override dates to work on normally-closed days |
| `day_hours` | Per-weekday hour overrides (e.g. `{ fri = 4 }`) |

See [Configuration](Configuration) for the full `config.toml` reference.

## Integration with Other Views

Changes made in the Team panel are reflected immediately across the extension:

- **Gantt Chart** -- the workload heatmap updates to show each member's capacity and allocation
- **Metrics** -- developer metrics cards and effort allocation charts reflect the current team composition
- **Dashboard** -- task counts and effort summaries incorporate assignee data

## Related

- [Configuration](Configuration) -- `config.toml` assignee settings reference
- [Gantt Chart](Gantt-Chart) -- workload view per assignee
- [Metrics](Metrics) -- per-member effort analytics
