# Changelog

All notable changes to the Handoff VSCode extension will be documented here.

## [0.12.0] — 2026-09-26

### Added

- **Requirements view** — A table-centric requirements view (works with handoff-mcp 0.36.0+): KPI summary (total / implemented / tested / verified / P0 not started), P0 alert banner, remaining-work summary, category progress, per-task coverage, and a sortable, filterable requirements table with an expandable detail panel (code and test references, linked tasks, jump to the document)
- **Requirements Explorer** — New sidebar tree grouped by category, priority or development stage, with "no tests" / "P0 only" / advanced filters and inline actions (set development stage, create a task for a requirement, open the requirement in its document, open code/test references, backfill stable IDs)
- **Verification matrix sub-items** — Requirement items in the document viewer with stable ID, priority and development stage; bulk check and bulk stage change; filter bar; linked-task badges
- **Coverage indicators** — Requirement coverage on Kanban cards, Gantt bars and the task detail's spec coverage section
- **Faster requirements loading** — Reads the requirement item list from handoff-mcp's `_requirements_summary.json` instead of opening every document

### Changed

- **Development stage badges** — Colour-coded by stage in the requirements table

### Fixed

- **Render errors** — Errors caught by the webview are now written to the "Handoff" output channel instead of being lost in the hidden webview console

## [0.11.0] — 2026-08-25

### Added

- **Multi-worktree overview** — When several AI agents work in separate git worktrees, the Dashboard shows active agents, claimed tasks with lease time, progress per worktree, merge status against `main` (merged / unmerged / conflict risk, with suggested merge order) and which session runs in which worktree
- **Worktree filter and session scope** — Filter the Task Explorer by worktree; sessions show their scope (primary / worktree / ephemeral); task locks and lease expiry are shown on tasks
- **Session-loop progress** — Progress of automated session loops is visible per worktree

## [0.10.2] — 2026-07-31

### Fixed

- **Malformed documents** — A document with broken YAML frontmatter is skipped and reported in the output channel instead of crashing the extension

## [0.10.1] — 2026-07-21

### Fixed

- **Stale views** — Data reloads when the panel or the task tree regains focus, so changes made by AI agents show up without a manual refresh

## [0.10.0] — 2026-07-19

### Added

- **Document graph** — Task nodes, shared-scope links, a verification-progress ring on each document, tooltips and an improved layout

### Changed

- **Document storage** — Documents are read from single Markdown files with YAML frontmatter (handoff-mcp's current format)

### Fixed

- **Gantt** — Drag dead zone, assignee filter reset, and the empty state of the workload heat gauge

## [0.9.0] — 2026-07-15

### Added

- **Document management** — Documents sidebar (grouped by type, with sections), a document viewer with rendered Markdown and section editing, cross-reference view in the bottom panel, and a document relationship graph

## [0.8.0] — 2026-07-08

### Added

- **Nested Workspace Support** — Recursive scan for `.handoff` directories across a workspace, with project grouping in the Task Explorer, project badges on task cards, and collision-safe task IDs across projects
- **Unified Project Filter** — A shared project selector now drives Dashboard, Gantt Chart, Metrics, Team Panel, and Session Timeline consistently, with selection persisted across reloads
- **Gantt Visibility Toggles** — Hide-completed toggle plus per-row hide/show with an individual restore popup, persisted in `config.toml`

### Changed

- **Projection Accuracy** — Done/skipped tasks now use `actual_hours` instead of `estimate_hours` in workload heat gauge, auto-scheduler leveling, and Team/Metrics panel stats, so future estimates aren't inflated by completed work

### Fixed

- **Project Selector Crash** — Switching projects while a Gantt assignee filter was active could blank the entire GUI. The root cause was a React rules-of-hooks violation (an early return before hooks in `GanttChart`); fixed by moving the empty-state guard into conditional JSX so hooks always run. Also added a root-level ErrorBoundary and defensive guards on `done_criteria`/`labels` access to contain future render crashes

## [0.7.0] — 2026-07-05

### Added

- **Multi-Session Support** — Session type extension with parent-child tree, fork/merge commands, session switching, and task session filter
- **Session Timeline** — SVG fork graph visualization (newest-first, git log style) with timeline filter
- **GUI Action Buttons** — Inline action buttons on task items (status, log time), session items (copy ID, fork, switch), and referral items (set status). Title bar buttons on Sessions and Referrals views
- **Session Status Grouping** — Sessions panel now groups by status (Active > Paused > Open > Closed) with collapsed Closed group, like the task explorer
- **Session Description** — Shows branch · commit · timeline info on each session row
- **Gantt Dependency Fixes** — Dependency clamping, group move undo, auto-schedule improvements
- **Dashboard Drill-Down** — Click KPI cards to filter, AI estimate multiplier dedup, metrics adjusted display
- **AI Estimate Multiplier** — Editable from settings and team panel
- **Effort Donut** — AI-adjusted display with overrun visualization
- **Session Loop v2** — Multi-agent workflow with parameterizable session-execute

### Fixed

- **Flaky Timer Test** — Increased timeout for flood test to prevent intermittent CI failure
- **Lint Environment** — Resolved WebView lint configuration issues
- **Auto-Schedule** — Fixed started_at handling and findSlot hang with cycle validation

## [0.6.0] — 2026-06-28

### Added

- **Timer Coordination** — MCP ⇄ VSCode bidirectional timer control via `.handoff/timer/` protocol. AI agents can now start, stop, pause, and resume the time tracker through handoff-mcp commands
- **MCP Activity-Aware Idle Detection** — Idle detection now considers MCP activity (timer requests from AI agents) alongside editor interactions. Idle time is excluded from elapsed tracking
- **Heartbeat & Authority** — VSCode publishes `authority.json` (owner + TTL) and `state.json` so the MCP server knows the extension is alive and can read current timer state
- **Request-Ack Protocol** — MCP writes command requests as JSON files; VSCode processes and deletes them (ack-by-deletion) with idempotency keys to prevent duplicate execution

### Fixed

- **Heartbeat Self-Feedback Loop** — Timer file watcher no longer watches `authority.json`, which the heartbeat loop writes every 10s. Previously this reset `lastActivityAt` and prevented idle detection from ever firing while a timer was tracking

## [0.5.2] — 2026-06-27

### Fixed

- Correct handoff-mcp link in empty-project welcome view

## [0.5.1] — 2026-06-26

### Changed

- Rename Marketplace displayName to 'Handoff MCP Dashboard'

## [0.5.0] — 2026-06-24

### Added

- **Dashboard** — Project overview with KPI cards, Kanban board, effort budget, daily closing, today's tasks, and recent activity feed
- **Gantt Chart** — Interactive timeline with drag-to-reschedule, milestone grouping, compare mode, progress line, and workload view
- **Metrics Panel** — Effort hours, velocity trends, session analytics, label/milestone breakdowns
- **Task Explorer** — Tree view with status icons, priority badges, milestone filtering, and context menu actions
- **Task Detail** — Done-criteria checklist, schedule, dependencies, time tracking
- **Time Tracker** — Start/stop timer with idle detection, linked to active task, persists across restarts
- **Session Browser** — Browse AI session history with summaries, decisions, blockers, and file pointers
- **Kanban Board** — Drag-and-drop status changes that write back to `.handoff/`
- **Effort Budget** — Configure total hours in `config.toml`, track burn rate on dashboard
- **Status Bar** — Task count and active timer display
- **i18n** — English and Japanese UI support
- **Auto-refresh** — File watcher on `.handoff/` with configurable interval
