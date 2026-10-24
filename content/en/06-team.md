---
title: Team · the debate hall
description: How a multi-seat debate runs: people, tickets, rounds, waiting for your signature, workflows and the record
section: Collaborate
order: 6
---

The **Team** tab is a table: several people and several AI seats in one discussion, a host
advancing the rounds, and a conclusion that **a human signs**. Three columns side by side —
seats present on the left, the feed in the middle, what needs you on the right.

## Seats

- **AI seats** — picked from your models; the host decides who speaks first and for how many rounds.
- **Human seats** — press "添加真人席位" (add a human seat) to issue a **ticket**, then send the join
  link. The other person opens it in their own browser and sees **this discussion only** — nothing
  else on your machine.

:::note A ticket is a scope, not a password
The ticket decides which discussion a person may enter. When it expires or is revoked, their page
says so plainly ("票据已失效，请让主持人重新发一张" — the ticket is no longer valid, ask the host
for a new one) instead of hanging on a spinner.
:::

Seat state is visible in the left column: **online**, **away**, **not joined**, **timed out without
speaking**. You never have to guess who is missing.

## How one discussion runs

1. The host opens it; the first round starts speaking, and the feed gets a rule
   `—— 第 1 轮 ——` ("round 1").
2. Each round, seats speak in turn; anyone can reply to a named seat ("回应 {name}").
3. In the final round the heading is **最终决策** (final decision) — that entry is not a conclusion,
   it is a proposal **waiting for your signature**.
4. The stop point reads "等待你拍板" (waiting for your call) and offers two buttons:
   **采纳拍板** (adopt it) or **继续讨论** (keep discussing). Adopting records
   "已采纳这个决策" (this decision was adopted) and stores who signed it.

A human seat has two settings: **permission** (may they speak, may they call it) and
**what to do when they don't show** (let AI write for them / skip and leave a trace / keep waiting,
with a timeout in seconds). The invite link is issued from the same panel.

The participant side uses different words: when it's their turn the page says "现在轮到你发言"
(it's your turn to speak), typing early tells them "发言会在轮到你时被采纳" (your message will be
picked up on your turn), and otherwise it shows "等 {name} 发言…" (waiting for {name}). Their
positions are: 提案 (propose), 支持 (support), 反对 (oppose), 反驳 (rebut), 补充 (add to),
决策 (decide).

:::warning Decisions don't adopt themselves
Only the entry you signed counts as the conclusion. In night mode (full autopilot) the system
adopts for you, and the feed states it explicitly: "夜间模式：决策已自动采纳". That is the
exception, not the default.
:::

## Board workflows

The Team tab can also run a workflow drawn on the board: nodes execute one by one with progress
written as `{ok}/{n} 节点成功` (nodes succeeded), and a failure stops there to say which node
broke — it never passes a half-run off as success.

## Every line is kept

Speech, rounds, signatures and tool calls are stored locally and travel with your backups (the four
debate tables are listed in [Projects & data](./12-projects-data.md)). Moving machines, restoring
history, or clearing one discussion alone all follow the two different rules in that chapter.

## Next

- To have work finished while you are away: [Office](./07-office.md).
- To see the tool calls behind each message: [Chat & approval](./05-chat-approval.md).
