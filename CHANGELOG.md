# Changelog

All notable changes to the Handoff VSCode extension will be documented here.

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
