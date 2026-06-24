# Time Tracker

The built-in time tracker records how long you spend on each task. It links directly to the active task and accumulates elapsed time into the task's `schedule.actual_hours` field.

## How It Works

The timer has four states:

```
idle ──start──→ tracking ──pause──→ paused
  ^                 |                  |
  └──── stop/cancel─┘──── stop ───────┘
```

- **Idle** — No timer running. Nothing shown in the status bar.
- **Tracking** — Timer is counting. The status bar shows elapsed time (e.g. `t1: 01:23:45`).
- **Paused** — Timer is suspended, either manually or by idle detection. Elapsed time is preserved.
- **Stopped** — Timer has ended. Accumulated time is written to the task's `actual_hours`.

## Automatic Start and Stop

When a task's status changes to `in_progress`, the timer starts automatically. When the status changes to anything else (done, review, blocked, etc.), the timer stops and the elapsed time is saved.

If you switch another task to `in_progress` while a timer is already running, the current timer stops (saving its time), and a new timer starts for the new task.

## Idle Detection

If VS Code loses focus for a configurable number of minutes, the timer pauses automatically. When you return, it resumes. This prevents inflated time records when you step away.

The timeout is controlled by the `handoff.timeTracker.idleTimeoutMinutes` setting (default: 5 minutes).

## Persistence

Timer state is saved automatically, so it survives restarts and crashes. When VS Code reopens, if the previously tracked task is still `in_progress`, the timer resumes from where it left off.

## Status Bar

While tracking, the status bar shows the active task ID and elapsed time:

```
Tracking:  t1: 01:23:45
Paused:    t1: 01:23:45 (paused)
Idle:      (not shown)
```

Click the status bar item to pause, resume, stop, or cancel the timer.

## Commands

All commands are available via the Command Palette:

| Command | Description |
|---------|-------------|
| `Handoff: Start Time Tracker` | Start timing the selected task |
| `Handoff: Pause Timer` | Pause the running timer |
| `Handoff: Stop Timer` | Stop the timer and save elapsed time to `actual_hours` |
| `Handoff: Cancel Timer` | Discard the current timer without saving |

## Where Time Is Stored

Elapsed time is added to the task's `schedule.actual_hours` field in the task JSON file. This is the same field used by the Dashboard, Metrics, and Effort Budget calculations. No separate time log is created — the value accumulates directly on the task.

## Related

- [Configuration](Configuration.md) — Timer-related settings
- [Dashboard](Dashboard.md) — Effort budget tracks actual vs estimated hours
- [Metrics](Metrics.md) — Velocity and effort analytics use `actual_hours`
