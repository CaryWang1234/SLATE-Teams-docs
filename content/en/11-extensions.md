---
title: Extensions
description: What each of the seven extension columns governs, what you can do in them, and what a reply mode or expert pack actually is
section: Capabilities
order: 11
---

Extensions is the fifth tab in the top bar, and its subtitle states the whole remit: **the capabilities available to a
model are decided on this page**. The left rail holds seven columns, each with a count; the rail number and the heading
number come from one source, so they change together.

| Column | What it governs | What you can do |
| --- | --- | --- |
| Skills | A written "how to do this kind of job" note for the model (SKILL.md) | Create, import from a local path, import from a GitHub repo, discover plugins in standard directories, delete, open one and try it |
| Tools | Resident backend capabilities, called through skill_run | Read-only list, open one to run it; **built-in tools cannot be deleted** |
| Modes | Reply modes | Four built-in tiers read-only; custom modes added, edited, deleted |
| New capabilities | Tools SLATE generated for itself, under `data/evolved/` | Enable / disable, roll back, revoke (source goes to history first) |
| MCP | Remote tools brought by external MCP servers | Add, connect / disconnect, delete, enable or disable per project |
| Expert packs | Persona + rules + knowledge base + skills bundled as one switchable expert | Create, import a zip, export, add or remove files inside |
| Actions | Process specifications | Create, edit, delete, roll back |

## Skills and tools are not the same thing

A **skill** is one SKILL.md: you write in plain language how this kind of job should be done, and after import the model
picks it up by task. **6** sample skills ship with the product (code review, commit message, design, research, weekly
report, Windows troubleshooting).

**Tools** are capabilities implemented in backend code. This column lists the **35** entries of the built-in registry —
reading and editing files, terminals and background tasks, generating PPT/Word/Excel/PDF, browser and desktop
automation, web search and page fetching. They are read-only here. What you *can* switch off is the set of features that
call a model on their own, under [Settings](./14-settings.md): **a capability switched off does not even appear in the
model's tool catalogue.** A separate group of in-conversation tools (board read/write, passing work between desks,
creating reply modes, closing out a target mode) is not listed there; the reply mode's tool whitelist decides those.

:::tip Adding a tool without writing one by hand
Use the tool factory (built-in tool `mcp_factory`) to generate one. It lands in `data/evolved/` and shows up in the
**New capabilities** column, where it can be disabled, rolled back or revoked at any time. Every overwrite, revocation
and rollback stores the previous content first; up to 5 versions are kept.
:::

## Reply mode

A reply mode decides **which prompt set this conversation uses, which tools are open, how many rounds it runs, how hard
it thinks and which model answers**. The four read-only built-ins are **smart** (full tool set), **chat** (no tools at
all, one round), **economy** (read-only tools only — it can see the project and skill catalogues but cannot write, run
a command or spend generation quota; low effort, 12 rounds) and **turbo** (full tool set, high effort, 40 rounds, no
stopping to ask).

A custom mode is a full specification: id, display name, icon, colour, appended prompt, tool whitelist ticked item by
item, reasoning effort, round limit and a chosen model (follows the current main model by default). The model can create
modes too — it calls `mode_write`, and the result lands in the same registry as your manual edits.

:::warning Don't conflate two things
Above the input box you change **which mode this conversation uses**; in the "Modes" column you change **what the mode
itself is**. Deleting a custom mode that is in use breaks nothing — those conversations fall back to the default mode.
:::

Approval mode (manual / auto / full access / night) is a different mechanism governing **whether commands and network
access ask you first**; its default is set in Settings, and [Chat & approval](./05-chat-approval.md) covers it.

## Expert pack

One expert pack = persona + behaviour rules + knowledge-base files + skill files, bundled as a single switchable whole.
**3** sample packs ship with the product. Two ways to use one: pick it from the expert selector under the input box to
inject it into this conversation, or attach it to an AI seat in the [Team](./06-team.md) tab.

## MCP and Actions

The MCP column connects to external servers; once connected their remote tools enter the model's view, and a remote tool
sharing a built-in name is overridden by the built-in. Each server can be disabled globally or enabled/disabled for the
current project alone (a project mask) — removing the mask returns it to the global configuration.

Actions are **process specifications**: routine operations written as required steps, which the model then follows. They
are stored as `data/actions/<id>.yml`, or in a project's own `.slate/actions/` where a same-named project Action wins.
Every overwrite keeps a backup, up to 5 versions, and can be rolled back; a stored version that no longer parses is not
allowed to be written back. In the [board's workflow view](./10-board.md), one Action is one runnable card.

## Next

- Which features call a model on their own, and how to switch each off: [Settings](./14-settings.md).
