# Lumi Social Studio — CRM

UGC creator business (Jasmine). Single-page React dashboard (`index.html`) that reads `crm-data.json` at runtime — no build step, no package manager.

## Files

| File | Purpose |
|------|---------|
| `crm-data.json` | Source of truth for pipeline, invoices, assets, calendar, action items |
| `index.html` | React SPA (CDN-loaded) that renders all dashboard views |

## crm-data.json structure

```
pipeline.sent[]       — pitches sent, awaiting reply       (ids: sNN)
pipeline.replied[]    — brands that have responded          (ids: rNN)
pipeline.bounced[]    — failed delivery / blocked           (ids: bNN)
pipeline.closedWon[]  — confirmed paid deals                (ids: wNN)
invoices[]            — invoice tracking
assets[]              — content deliverables
calendarEvents[]      — scheduled events
actionRequired[]      — bounced brands needing IG DM outreach
```

## Routine: crm-email-sync

Scheduled at 07:00 and 14:00 AEST (04:00 and 21:00 UTC) via `.claude/settings.json`.

Each run: scans Gmail inbox + sent for the last 12 hours, updates `pipeline` statuses, commits and pushes `crm-data.json`, and sends a push notification if anything changed.

Full execution instructions are embedded in the routine prompt inside `.claude/settings.json`.

## Git

Working branch: `claude/affectionate-dirac-5h0xx4`
Always push to this branch. Never push to main directly.
