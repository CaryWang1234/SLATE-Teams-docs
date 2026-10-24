---
title: Interface & tabs
description: What each of the five tabs holds, the Chat and Desks sides of Office, the three columns of the team page, light/dark plus the ten theme presets, language and the Prompt Factory entry
section: Start
order: 3
---

One topbar over one workspace. Five tabs sit in the middle of the topbar; four buttons on the right:
**Keys**, **Remote**, **Theme**, **Settings**.

## The five tabs

| Tab | What it holds | Read |
| --- | --- | --- |
| Office | One page, two sides: **Chat** is the ordinary one-to-one conversation (sidebar, message feed, usage strip, input toolbar); **Desks** is the AI staff roster, the virtual office and the hand-off composer, with five tabs on the right: Activity / Waiting on you / Duties / Role / Standup & Record | [Chat & approvals](./05-chat-approval.md) · [Office](./07-office.md) |
| Team | The debate hall: seats present, the feed, awaiting your signature | [Team](./06-team.md) |
| Whiteboard | Cards as a reasoning chain plus a freehand layer; five views: Git / Flow / Kanban / Outline / Workflow | [Whiteboard](./10-board.md) |
| Extensions | The master switch for everything the model may use, in seven sections: skills (SKILL.md), tools, modes, new features, MCP servers, expert packs, Actions | [Extensions](./11-extensions.md) |
| Settings | Models and keys, context and project, approval mode, theme, notifications, backup and storage, one block after another | [Settings](./14-settings.md) |

:::note The two Office sides are not two tabs
The Office tab has a **Chat / Desks** switch at its top right, and it opens on Chat.
Inside Chat, "Project / Tasks / Summary" is a column **inside** the page; switching them never leaves
the conversation. The right rail stacks the task list, background tasks and the Grind panel, each
opening and closing on its own.
:::

## The three columns of the team page

Three columns, one per question a meeting table asks:

- **Left · Present** — who is at the table (AI seats and [human seats](./06-team.md)), then "Team preset"
  and "Team history". History lives here too because both answer the same thing: how this session was assembled.
- **Middle · The feed** — the topic field, the max round count, this session's usage strip, and two views
  underneath: Team discussion / Workflow.
- **Right · Awaiting You** — the host-only actions: the "Decisions need my sign-off" switch and the items
  waiting on you.

## Theme

Two built-in themes: **light** and **dark**. The "Theme" button in the topbar switches them; the shortcut
is `Ctrl+D` (`⌘D` on macOS).

Below that sits the **custom theme** (Settings → Custom theme): you fill only four source colors —
page background, panel background, body text, accent — and the other thirty-odd tokens are derived from
them by luminance and contrast, so every text level stays readable. The same block handles panel
opacity, imported font files and a background image (or whatever Wallpaper Engine is currently showing).

:::tip There are ten presets
The preset row offers **ten** complete source sets: Ledger paper, Ink night, Mist blue, Deep sea, Pine ink,
Moss, Clay, Dusk plum, Graphite, Letterpress. Clicking one fills the palette below; you can still edit
each swatch — and once you do, it no longer belongs to any preset.
:::

While a custom theme is on, light/dark is locked: the topbar button and `Ctrl+D` do nothing, and clicking
the button says why. Turning the custom theme off removes the whole injected stylesheet, down to the pixel.

## Interface language

**There is no language switch inside the app.** The language is chosen at install time; the installer writes
it to `data/language.txt` (`zh` or `en`) and the runtime only reads it.

To change it: edit `data/language.txt`, or start with the `SLATE_LANG` environment variable (higher priority),
then restart.

Translation covers interface text only — including button tooltips and input placeholders. Model output,
your own input and code blocks are never translated.

## Prompt Factory

It no longer owns a tab. The entry is the **Open Workbench** button under **Settings → Context & Project**.

The factory folds the constitution summary, context snippets, task description, constraints and deliverable
requirements into one prompt you can actually hand over. Closing it only hides the form: your draft, the files
you ticked and the generated result are all still there when you reopen it.

## Next

1. [Models & usage](./04-models.md) — add one model, read the usage strip.
2. [Chat & approvals](./05-chat-approval.md) — how many approval modes there really are, and what each blocks.
