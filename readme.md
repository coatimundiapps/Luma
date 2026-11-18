# Luma

**A modern calendar for Deepin Linux.**

Luma is a lightweight, good-looking calendar written in Python with **GTK 4** and **libadwaita**, designed to fit seamlessly into the Deepin Desktop Environment while staying usable on any GTK4 desktop. It syncs with your online calendars over **CalDAV**, supports read-only **.ics subscriptions**, handles **recurring events** properly, and follows your system's accent colour and dark/light preference automatically.

## Features

**Four views, one date model**
- **Month** grid with drag-and-drop between days and a clickable “+N” overflow popover.
- **Week** and **Day** time grids (1440 px) with column layout for overlapping events, vertical drag to move, edge handles to resize, and an all-day band.
- **Agenda**: a rolling 30-day list, grouped by day, with multi-day events repeated on every day they cover.

**Real online sync**
- **CalDAV** accounts (Google, Infomaniak, Nextcloud, Radicale…) with two-way sync.
- Read-only **.ics subscriptions** (public holidays, school calendars, feeds…).
- Per-calendar visibility and enable/disable toggles, local renaming, and per-category colouring.
- Range-bounded server queries (`date_search`) so syncing stays fast on big accounts.

**Recurrence done right (RFC 5545)**
- `RRULE`, `EXDATE` and per-occurrence overrides (`RECURRENCE-ID`) fully supported.
- Edit **this occurrence**, **all occurrences**, or **this and following** — with the correct scope prompt on drag and resize.
- Series anchors are preserved when you edit an occurrence, and unknown `RRULE` parts (`INTERVAL`, `BYDAY`, `COUNT`…) survive round-trips instead of being silently truncated.
- Local timezone (IANA, DST-aware) and exclusive `DTEND` for all-day events, with `VTIMEZONE` blocks generated on demand.

**Organisation**
- Colour-coded **categories** (rubriques) that map onto calendars.
- Reminders (30 min / 1 h / 1 day before) delivered by a background **daemon** that also expands recurring events.
- Full-text search across the visible range, with jump-to-result.

**Deepin integration**
- Accent colour and dark mode read live from the DDE portal / `org.deepin.dde.Appearance1`, with graceful fallbacks on other desktops.
- A **dynamic day icon** regenerated each morning, so the taskbar/dock shows today’s date.
- Keyboard shortcuts for views, navigation and “today”.

**Built to not lose your data**
- Atomic JSON writes with rotation and recovery from a corrupted cache.
- Stable calendar IDs derived from URLs (never from server ordering).
- Deletion tombstones so removed events don’t resurrect on the next sync.
- Offline-safe merge: events created while disconnected are kept, not overwritten.
- Passwords stored in the system keyring (**libsecret**), with a `0600` file fallback.

**Internationalisation**
- gettext-based, with a language selector in Settings and 9 locales declared (French shipped; others welcome via pull request).

## Tech stack

- **Python 3** · **GTK 4** · **libadwaita**
- [`python-caldav`](https://pypi.org/project/caldav/) + [`icalendar`](https://pypi.org/project/icalendar/) for sync and iCalendar parsing
- `python-dateutil` for recurrence expansion
- Clean internal separation: `recurrence.py` and `ical.py` are pure, network-free, unit-tested modules; `crud_mixin.py` shares one CRUD implementation across all four views; `events_store.py` / `storage.py` / `secrets_store.py` own persistence and security.

## Status

Luma is a personal project by **CoatiMundi**, packaged as a `.deb` for Deepin. Contributions, translations and bug reports are very welcome.


*** INFORMATION : Application designed specifically for Deepin Linux. Use on other Linux distributions is not guaranteed. ***

