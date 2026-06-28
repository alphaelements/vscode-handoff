# Changelog

All notable changes to the Handoff VSCode extension will be documented here.

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
