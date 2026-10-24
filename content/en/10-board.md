---
title: The board and workflows
description: Cards and logic chains on the board, its five views, and exactly what a workflow run writes to the screen
section: Capabilities
order: 10
---

The board is the fourth tab in the top bar, and it is **one global** board: cards, connectors, freehand strokes and text
notes stack as four layers on one canvas. It is not split per conversation — its contents are stored with your local
settings and are still there when you switch.

## How cards form a logic chain

A card carries four things: a **title**, a **description**, a **colour tag**, and **arrow targets** (target card IDs,
comma-separated). Double-click a card to edit it in place, drag it to move it, or use the **connect** tool and click two
cards to add an edge. Colour is not decoration: red is risk, orange to do, yellow an idea, green done, blue information,
purple creative, default unclassified.

Arrows express dependency and data flow. The kanban view columns cards by colour, the flow view links them into a graph,
the outline view collapses parent-child levels, and the Git view reads your repo's commits. All five view buttons sit in
the board header and it opens on **kanban**. The toolbar adds pen and text as free layers, with undo-stroke and
clear-strokes; header buttons are add card, auto-arrange layout, return to content, AI-organise into a flow chart,
show/hide the flow chart (Mermaid), export, clear.

:::note AI-organise is gated
"AI-organise into a flow chart" is one of the [AI-assisted features](./14-settings.md). Turn it off and the button only
explains why — it never sends your board to a model.
:::

## The workflow view on the board

This column is not a DAG editor. It is three things on one screen:

1. **A run control bar** — state reads `空闲` (idle), `运行中 · 第 {n} 轮` (running, round n), `已完成` (done),
   `已中断` (aborted), with elapsed time beside it, and buttons for stop, run it out, auto-advance, reply mode, thinking
   effort and "go to team". When this conversation has never run, the list keeps a line saying `本场还没有运行记录`
   instead of leaving the previous run's tail on screen.
2. **Current run** — every tool call this round, with status `进行中` / `完成` / `失败` / `已取消`, under a heading of
   `当前运行 · {finished}/{total}`.
3. **Process-spec cards** — one Action per card, labelled 共 {n} 步 (n steps), {n} 项输入 (n inputs), 产出落到…
   (output lands in …). Expand its steps in place, press 运行此流程 to send it into the conversation as an @-mention, or
   pin it. The author line reads 用户编写 (written by you) or 模型编写 (written by the model).

Below them sits the **team star map**: the conversation is the centre star, each member a planet, real hand-offs between
members drawn as arcs. With no team record for this conversation it says so plainly and tells you where to start one.

## DAG workflows run on the Team tab

The thing that executes node by node lives in the **workflow** column of the [Team](./06-team.md) tab — a tab beside
"team debate".

- Definitions are JSON files; **8** ship built-in under `backend/workflows/`, and an empty list writes the path to drop
  them in on the screen.
- The task goes in first and reaches every node as `$input`; without it the run refuses to start and says so.
- Node states read `等待` / `运行中` / `成功` / `失败` / `跳过`; nodes with no dependency between them run **in
  parallel**, and progress reads `运行中（{done}/{n}）…`.
- The finished line is `{ok}/{n} 节点成功 · 产物已写入知识库（{title}），可在记忆面板查看` — "{ok}/{n} nodes
  succeeded, output written to the knowledge base, viewable in the Memory panel". If every node passed but the write
  failed, it becomes `节点成功 {ok}/{n}，但写入知识库失败: {msg}`: **a half run is never reported as success**.
- A failed or skipped upstream node skips everything downstream and names who was responsible. A cycle is reported as
  `DAG 存在环，涉及节点: {nodes}` and that workflow does not run.
- A node bound to neither a team member nor an explicit model falls back to the default set under "AI-assisted features
  → team workflow execution"; a bound node keeps its own binding. A node with no usable model fails outright.

:::warning Run output lands in the knowledge base
Each run becomes one entry titled `工作流产物 · {workflow}` carrying every node's status, elapsed time, error and output
summary. Find it in the [memory panel](./12-projects-data.md) — not on the board.
:::

## Next

- Creating and rolling back an Action: [Extensions](./11-extensions.md).
- The switch and default model for workflow execution: [Settings](./14-settings.md).
