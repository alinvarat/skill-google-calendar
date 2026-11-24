---
name: google-calendar
description: Read or change Google Calendar events, availability and recurring schedules; sync a compatible widget when requested.
---

# Google Calendar

1. Use an available Calendar connector/MCP first; inspect its actual tool schema. Check account and calendar with read-only profile/list tools. Do not assume an old login, event ID or a tool name from another host is valid.
2. Search/read the target event before changing it. Distinguish a whole recurring series from one instance. Use Asia/Bangkok (+07:00) by default and explicit dates. Check availability before scheduling when supported. Ask only if the intended recurrence scope remains unclear.
3. Apply only the requested change. Inviting/notifying others requires authorization for that communication. After a timeout: search/read actual state. If the intended event exists with correct fields, return it unchanged; do not update or recreate it. Correct fields only if the original request requires that correction. Retry create once only after absence is established; if lookup is inconclusive, report uncertain state and stop.
4. Read back the saved event and report the result. Separate a calendar success from a failed widget sync.

If no connector exists, run `command -v gcalendar`, then `gcalendar --help`; report a missing command or auth instead of claiming readiness. On Debian do not call PowerShell, `.cmd` or `%APPDATA%` paths. Sync a widget only after verifying its installed Linux command.

On Windows only, read [legacy CLI/widget reference](references/windows-legacy.md) and recheck paths, account and event IDs before use. For unknown host tools, use the tools your host actually provides.
