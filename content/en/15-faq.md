---
title: FAQ
description: Won't start, can't connect, work won't run, numbers don't add up — twelve questions with answers that actually exist in the code
section: Data & settings
order: 15
---

Every answer here traces back to a line of code. Anything we couldn't verify isn't in this list.

## Won't start, won't connect

**Double-clicking does nothing, or the backend won't come up.** If the first instance is still
opening its window or is hiding in the tray, another launch calls it back and prints "already
running". When it really fails, the port is usually taken: the app prefers 8130 and falls back to a
free one, and remote control prefers 8131 and walks up twenty ports. Both use the port they
**actually** got, so the address on screen is the truth and nothing else needs editing.

**Which file holds the logs.** The backend and the launch sequence write `desktop_backend.log`: at
the repo root when running from source, next to the program folder on a Windows install, inside the
data folder on a macOS install. Errors thrown by the page itself go to `data/js_errors.log`.

**A phone opens the address and hits "authorization required", or it worked yesterday.** The first
case is an address without its auth code — copy it fresh from the host's settings or scan the QR
code. The second is that the master auth code is generated anew for every process, so a restart
retires the old link. Unauthenticated LAN access is refused on purpose.

## The interface

**How do I switch the interface language?** You don't switch inside the app: the language is chosen
at install time and written to `data/language.txt`. Edit that to `en` or `zh`, or override it once
with the `SLATE_LANG` environment variable, then restart.

**The red-ink side is hard to read in dark mode.** Alert red, done green and to-do amber are not
driven by your accent colour: a light set and a dark set exist and the page picks one by background
luminance, custom themes included. The ledger red is deliberately deep and dull on light and swaps
to a brighter value on dark, so "darker means less visible" never happens.

## Office and debate hall

**Why isn't an AI staff member's work running?** The backend only queues; it executes nothing. The
one on duty is the page that is open on that machine. Close every page and jobs stay in the queue;
an expired lease returns a job to the queue, and the same job is claimed at most twice before it is
declared failed. A phone page has no office, so a phone is never on duty.

**Where does work go once it is judged "not worth doing"?** Into "waiting on you", with the reason
written on the line. It isn't a failure and the backend never revives it: there are exactly two
exits — you put it back in the queue (raised above ordinary duty work, though triage can still
outrank it), or you agree it shouldn't be done and it closes. An employee can't open that door.

**The daily budget is full, so why did my own hand-off still schedule?** The circuit breaker answers
one question only: "may the duty roster queue **new** work". Already-queued jobs finish (cutting one
half-way costs more and explains less), morning triage still runs — that is precisely the judgement
of "what to do with the budget left" — and the button you pressed is your call to make.

**Why did the note get worked again on the next pass?** That "open item" note was never struck
through. When he writes a new note, he has to name the one it closes. Each person keeps only the
forty most recent notes; unlimited history would fill his own context first.

**The participant's page says the ticket is no longer valid.** Have the host issue a new one.
Tickets can be revoked and the database stores only their hash, so a revoked link is dead for good —
the original string can't be recovered from a backup either.

## Data

**"Clear conversations" left my staff in place, and a restore reported 0 rows.** Both are designed.
The roster, the duty schedules and an employee's own notes count as **configuration**, not history.
A 0-row restore means that backup never carried the block: the tables are now created before
merging so a clean machine doesn't silently drop whole pieces of history, but exports made before
those tables existed genuinely have nothing to give back — export again.

**Is my key in the backup?** Not in the backend half (the tables); **yes** in the local half, which
is plaintext. Conversely, nothing under `data/` that is configuration or a binary is in there:
shared desktop settings, MCP endpoints and their secrets, scheduled tasks, skills, expert packs,
action playbooks, the global constitution, the knowledge base, background images and imported fonts.
Move those yourself.

## Next

- Install methods and the port split: [Install & launch](./02-install.md).
- The full backup scope: [Projects, backups and the ledger](./12-projects-data.md).
- Remote control and headless mode: [Phone remote control](./13-mobile.md).
