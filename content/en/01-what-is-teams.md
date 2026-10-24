---
title: What SLATE Teams is
description: SLATE Teams in one page: people and AI at one table, what the debate hall, the office and the ledger each own
section: Start
order: 1
---

SLATE Teams runs on **your own machine**. No server, nothing uploaded, model keys stay local.
It makes one thing easy: several people and a crew of AI working at the same table — with a
trace left behind for every decision.

The wordmark is 席, which means both a seat at the table and the act of taking one. The
interface follows the "Ledger" identity: graphite paper, red-ink annotations, square corners,
hairline rules like a ledger page.

## The three things it is for

| Where | What it owns | Read |
| --- | --- | --- |
| Debate hall | People and AI seats in one discussion; the host advances rounds; conclusions need a signature | [Team](./06-team.md) |
| Office | AI staff pick up work on their shift, every delivery passes a review, cost lands per employee | [Office](./07-office.md) |
| Ledger | Who said it, who approved it, how many tokens — stored, exportable, restorable | [Projects & data](./12-projects-data.md) |

:::note In one line
The debate hall is collaboration **at the same moment** — everyone in one discussion. The office
is collaboration **at different moments** — you leave the work, an AI staff member does it on
shift, you check it when you're back.
:::

## Six top-level tabs

- **Chat** — the ordinary one-to-one conversation: tool calls, approvals, context budget.
- **Team** — the debate hall. Seats, the feed, and "waiting for your signature" in three columns.
- **Office** — AI staff roster, duty schedule, hand-offs between desks, the delivery queue.
- **Board** — spread a discussion into a reasoning chain and workflow nodes.
- **Extensions** — skills, MCP servers, built-in tools, reply modes, experts: capabilities live here.
- **Settings** — models, theme, language, data & privacy, and each token-spending AI feature.

## How it relates to SLATE

SLATE Teams is a sibling of [SLATE](https://slate-ai.site/). They share the base — chat, tools,
skills, board, data layer — and differ in the **collaboration layer**: multi-seat debates,
tickets with narrowed scope, AI staff on a duty roster.

Both install on one machine: ports, data directories, installer identity and update feeds are
separate, so neither overwrites the other and no configuration is shared.

:::tip Which one first
If it's only you, SLATE is lighter. If you want people in the same discussion, or AI working by
shift, use SLATE Teams.
:::

## Where your data is

Every conversation, seat, job, message and ledger entry lives in `data/` inside the install
directory as local SQLite files. Offline means no requests; the network is used only when you
call a model API or check for updates.

How to back it up — and why the two "clear" buttons are not the same thing — is in
[Projects & data](./12-projects-data.md).

## Next

1. [Install & launch](./02-install.md) — set it up, add one model, open the first table.
2. [Interface & tabs](./03-interface.md) — what each of the six tabs holds, light and dark.
3. [Office & AI staff](./07-office.md) — the part that is genuinely different here.
