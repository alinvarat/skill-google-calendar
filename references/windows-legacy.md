# Windows gcalendar and widget reference

Use only on Windows after verifying `gcalendar --help`, the connected account, and current event details. Always re-fetch event IDs; do not reuse remembered ones.

## Common Workflows & Commands

### 1. Inspect Calendars and Events (Read-Only)
```bash
# View today's schedule
gcalendar readonly today

# List events in a specific time range (RFC3339)
gcalendar readonly events --start 2026-11-09T00:00:00+07:00 --end 2026-11-16T00:00:00+07:00 --max 50

# Keyword search
gcalendar readonly search "<keyword>"

# Inspect full event details and recurrence rules
gcalendar readonly get [EVENT_ID] --json

# List available calendars
gcalendar readonly calendars
```

### 2. Update Recurring Events (Mutate / Update RRULE)
To extend or modify recurring schedules (e.g., class timetable):
```bash
# Update RRULE on parent series (target series parent ID, not individual instance)
gcalendar mutate update [EVENT_ID] --rrule "FREQ=WEEKLY;UNTIL=20261115T170000Z;BYDAY=MO,TU,WE,FR"
```

### 3. Create Events
```bash
# Standard single event
gcalendar mutate create --summary "Meeting Title" --start 2026-11-10T10:00:00+07:00 --end 2026-11-10T11:00:00+07:00

# Recurring event
gcalendar mutate recurring "Series Title" --start 2026-11-10T08:00:00+07:00 --end 2026-11-10T11:00:00+07:00 --rrule "FREQ=WEEKLY;UNTIL=20261231T170000Z;BYDAY=MO,WE,FR"
```

---

## Recurring series
Fetch the parent series ID with `gcalendar readonly search` / `get --json` before updating; never reuse event IDs from notes.

---

## Desktop Calendar Widget Sync
- **Widget script**: `cal_widget.py` (top-right frosted-glass widget)
- **Data cache**: `%APPDATA%\gcal-desktop-widget\data.js`
- **Sync script**: `%APPDATA%\gcal-desktop-widget\update.ps1`
- When modifying calendar events, trigger an immediate local cache sync by running:
```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File "$env:APPDATA\gcal-desktop-widget\update.ps1"
```
*(The widget also refreshes automatically every 10 minutes or on right-click)*
