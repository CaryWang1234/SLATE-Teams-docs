---
title: Projects, backups and the ledger
description: What a workspace and its "current root" really mean, which tables a backup carries, and how restore and the two kinds of clearing differ
section: Data & settings
order: 12
---

Teams keeps its things in three layers: **the view** (which project you're looking at), **the
records** (tables in the chat database) and **the configuration** (files under `data/`, plus the
`.slate/` inside your project). One backup moves only part of the first two.

## Projects and workspaces

- A **single-folder project** is just that folder. A **workspace** is a host folder holding the
  configuration, whose members are several unrelated folders. The host lands at
  `data/workspaces/<name>`, its configuration is `<host>/.slate/config.json`, holding three things:
  what it is, the member list, the current root.
- There is **one current root at a time**. Switching it changes that one value; files, Git and the
  terminal working directory follow. Where configuration gets read and written is tracked
  separately, so a workspace's settings never land in a member's own `.slate/`.
- Everything registered stays in `data/projects.json`, and **the one you're looking at** is still
  unique. Identity comes from the absolute path of the host folder — move it and the identity
  changes, which is why each entry carries aliases to re-file old conversations by hand.
- Conversations attach to a project **id**, not a name. SLATE's own per-project data goes to
  `data/projects/<id>/`, never into your repo.

## What a backup actually carries

An export is one JSON file with a version number and three parts: the backend tables, your browser's local blob, and the team history list.

| Group | Tables | Inside |
| --- | --- | --- |
| Chat | conversations, messages | sessions and messages, archived ones included |
| Memory | memories, prompt_snippets | long-term memory, prompt material |
| Four debate tables | team_sessions, team_turns, team_attendees, team_inbox | each debate's header and seat snapshot, full speech text, tickets (sha256 only), turns waiting to be collected |
| Two ledger tables | runs, tool_events | the accounts per pass and every tool call; the star map and "which files changed" count from here |
| Two office tables | office_jobs, office_messages | the delivery queue and desk messages |
| Daily accounts | daily_usage | tokens per day; without it sessions restore fine and the activity heatmap stays blank |
| Three roster tables | employees, employee_duties, employee_notes | AI staff, duty schedules, their own notes |

:::note Everything from the debate tables down is what Teams adds over upstream
A missing table always shows up the same way: **the backup looks complete, and that block is empty
after the restore**. So every new table declares itself — record or configuration.
:::

## Two ordering traps when restoring

- **Create the tables first, then merge.** The debate, ledger and office tables are built lazily by
  whichever endpoint touches them first, so on a clean machine that never opened the team tab and
  never hired anyone they don't exist at all. Skip that and they all read as "no data": the count
  comes back 0 while the screen still says "done".
- **Merge only what's new.** Rows go in by primary or natural key; an existing row is skipped, never
  overwritten. The speech and tool-event tables drop their row numbers first — the same utterance
  is the same (session, sequence) pair on both machines, and reusing the id would collide with a
  locally written row and get silently swallowed.
- The page reloads once after an import: the local half only takes effect on reload.

## The two "clear" actions are not the same

| Where you click | What goes | What stays |
| --- | --- | --- |
| Task list, "clear all sessions" | Sessions and messages | The debate text and delivery history, with only their references to these sessions blanked out |
| Settings, storage, "clear conversations" | Messages, sessions, the four debate tables, the two ledger tables, the two office tables, the daily accounts — then the database is compacted | Employees, duty schedules and their notes; memory and prompt material; the knowledge base |

:::warning The second one takes the debate and the deliveries with it
The confirmation has to say that in full. The roster and the schedules are **configuration**, not
history: nobody says "clear conversations" meaning "fire my staff and cancel their shifts".
:::

## What stays out of the JSON on purpose

Configuration and binaries under `data/` aren't backed up: `desktop_state.json`,
`mcp_servers.json` (MCP endpoints and secrets), `scheduled_tasks.json`, `skills/`, `experts/`,
`actions/`, `constitution.json`, `knowledge.db`, `data/theme/` (background images, imported fonts),
the registry and its hosts. A project's own `.slate/` travels with the code instead.

:::danger The backup file is plaintext
The local half carries the model keys you typed in. Don't commit it, don't share it carelessly.
:::

## Next

- Keep working from another machine: [Phone remote control](./13-mobile.md).
- Where the switches a backup doesn't carry live: [Settings](./14-settings.md).
- When something went wrong anyway: [FAQ](./15-faq.md).
