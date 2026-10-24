---
title: Chat & approvals
description: What the Office chat view can do, the four real approval modes and what each lets through, the exact meaning of Night Mode, where the high-risk lists live, how tool calls render
section: Daily
order: 5
---

## What the Office chat view does

Open Office in the top bar and you land here by default. The switch at the top right goes to **Desks** —
the AI staff office. They are two sides of one page, not two separate tables.

- **Sidebar**, three tabs: Project (folder and file tree), Tasks (past conversations — searchable, batch manageable,
  archivable), Summary.
- **Above the feed**: manual context compaction, memory & profile, expert packs, prompt snippets, task list, background tasks.
- **Input toolbar, left**: the "+" popover — Grind Mode, Brainstorm, Target Mode, Scheduled Tasks, plus Mentions
  (@ prefix) for skills / tools / MCP / files. Then response mode, approval mode, attachment, model, reasoning effort.
- **Input toolbar, right**: Polish prompt, Voice Input, Send. `Enter` sends, `Shift+Enter` breaks a line.

Four built-in response modes: Smart, Chat, Economy, Turbo. They differ in whether the tool catalog goes out, how many
rounds they get and which prompt they append; custom modes live on the [Extensions](./11-extensions.md) page.

## Approval modes: four of them

The pill at the lower left of the input box is approval mode. There are **four**, changeable at any time, and the change
applies to **this conversation only**:

| id | Label | Lets through | Stops |
| --- | --- | --- | --- |
| `ask` | Manual Approval | Tools that never cross this gate, like local file reads and writes | Asks before **every** command and every network call |
| `auto` | Auto Approval | Commands and network calls matching no high-risk rule | Asks only when one does |
| `full` | Full Access | Never asks for commands or network | Still asks when a condition is missing; catastrophic commands stay hard-blocked |
| `night` | Night Mode | Commands, network and questions all go unanswered | Only catastrophic commands |

`ask` is the default for new conversations. Settings → Approval Mode changes that default; a conversation that has
picked one stops following it.

:::note Only five things cross this gate
terminal running a command, bg_task starting a job (status / log / stop change nothing, so they don't count), web_search,
web_fetch, browser_automation. Local file reads and writes never come here.
:::

## What Night Mode actually means

The **unattended** tier: the same pass-through rule as Full Access, plus the "ask one multiple-choice question when a condition is missing" path switched off too. No question pops — the model picks an option itself, writes the choice and its reason into its reply, and continues.

It adds no new rule and opens no new door — the only difference is that nothing is waiting for a person. Pair it with
"Keep the system awake while Night Mode tasks run" (Settings → Approval Mode, on by default).

:::warning Catastrophic commands are blocked in every mode
The backend refuses these prefixes with no override, approval included: `rm -rf /`, `rm -rf ~`, `format c:`, `format d:`,
`mkfs`, `dd if=`. Full Access is marked red (no safety net); Night Mode night purple (the night is handed over).
:::

## Where the high-risk lists live

One list, mirrored on both sides — change both or they drift:

- Frontend: `HIGH_RISK_PATTERNS` in `frontend/js/services/riskguard.js`, plus one check for "downloaded and piped
  straight into a shell".
- Backend: `HIGH_RISK_PATTERNS` in `backend/skills/terminal.py` (one more rule, the PowerShell `ri` alias) and `BLOCKED_PREFIXES`.

The rules are hard-coded: file and directory deletion, disk writes and partitioning, shutdown and reboot, privilege
escalation, forced kills, the registry, services and accounts, file permissions, Git force-push / hard reset / clean /
branch delete, database drops and truncates, global dependency removal. Each command is split on `&&`, `||`, `;` and `|`
and checked segment by segment, so a rule buried in a chain cannot slip through.

## What the approval dialog shows

Three titles: High-Risk Command Approval / Command Approval / Network Access Approval. It states the triggered rule or the
current mode, prints the command or the access target, and for commands has the current model explain what the command does
(turn that off under Settings → AI features). The button reads "Approve & Run" or "Allow access".

Under parallel runs several dialogs **queue** rather than quietly refusing each other, so nothing is rejected before you've
seen it. A refusal goes back to the model verbatim, with an explicit instruction not to retry the same call.

## How tool calls render

Each call is a card: tool icon, name, a one-line summary, and a status pill reading executed, applied, created, appended,
diff preview, file preview, append preview, failed, or not run. Cards are **collapsed by default**; only a failed one opens
on its own. Click for the arguments and output — for file edits that means the path and the edit count, never the whole
diff. Images, videos and documents a tool produced get a preview inside the card, and several calls in one turn group under
a heading reading "{n} calls", listing the first three tool names.

## Next

- To have AI keep working while you're away: [Office](./07-office.md).
- How the context budget is computed: [Models & usage](./04-models.md).
