# Session Browser

The Session Browser lets you review the history of AI coding sessions managed by [handoff-mcp](https://github.com/alphaelements/handoff-mcp). Each session captures what was accomplished, what decisions were made, and what the next session should pick up.

## Session List (Sidebar)

Sessions appear in the sidebar below the Task Explorer, listed in reverse chronological order. Each entry shows the session date and a one-line summary.

Session indicators:

| State | Indicator | Meaning |
|-------|-----------|---------|
| Active | Pulsing dot | A session is currently running |
| Paused | Solid dot | Session was suspended mid-work |
| Closed | No dot | Session completed normally |

Click any session to open its detail panel.

## Session Detail Panel

The detail panel shows the full context of a session:

### Summary
A one-line description of what was accomplished during the session.

### Decisions
Key decisions made during the session, each with:
- **What** was decided
- **Why** (the reasoning)
- **Confidence level** — `confirmed` (verified by testing), `estimated` (reasoned but not verified), or `unverified` (hypothesis)

### Blockers
Issues that prevented progress. These carry forward to the next session as priority items.

### Checklist
Verification items with ownership:
- **AI-owned** items — the next AI session should handle these
- **User-owned** items — require human action (e.g. manual QA, approval)

Each item is marked checked or unchecked.

### Handoff Notes
Contextual notes for the next session, categorized as:
- **Context** — Background information needed to continue
- **Caution** — Risks or constraints the next session must respect
- **Suggestion** — Concrete next actions to take

### File References
Links to files and line ranges relevant to the session's work, so the next session knows where to look.

## Referrals Sidebar

The sidebar includes a dedicated **Referrals** section (below Sessions) that lists all incoming cross-project referrals. When work in one project reveals an issue or improvement needed in another, handoff-mcp creates a referral and delivers it to the target project's `.handoff/referrals/` directory.

Each referral entry shows the source project, type, and priority. Click a referral to open its detail panel.

### Referral Detail

The detail panel displays:

- **Source project** — Which project sent the referral
- **Type** — `bug` (defect report), `improvement` (enhancement suggestion), or `info` (informational notice)
- **Priority** — High, medium, or low
- **Summary and details** — Full description of the issue
- **Associated tasks** — If the referral includes suggested tasks with done criteria
- **Context** — Branch, commit, error logs, or other data the source project attached

### Referral Status

Use **Handoff: Set Referral Status** from the Command Palette or right-click a referral in the sidebar to change its status:

| Status | Meaning |
|--------|---------|
| **Open** | Not yet reviewed |
| **Acknowledged** | Reviewed; work not yet started |
| **Resolved** | Issue addressed or dismissed |

### How Referrals Are Created

Referrals are created by [handoff-mcp](https://github.com/alphaelements/handoff-mcp) during AI sessions, not by the extension. The extension reads referral data from `.handoff/referrals/` and provides a read + status-update interface.

## How Sessions Are Created

Sessions are not created by the extension itself. They are produced by [handoff-mcp](https://github.com/alphaelements/handoff-mcp) during AI coding sessions (e.g. with Claude Code or similar tools). The extension reads and displays the session data stored in `.handoff/sessions/`.

## Related

- [Getting Started](Getting-Started.md) — How to set up handoff-mcp
- [Task Explorer](Task-Explorer.md) — Tasks referenced by sessions appear in the tree view
- [Configuration](Configuration.md) — Settings for auto-refresh and locale
