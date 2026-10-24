---
title: Office · hiring, rosters, deliveries
description: How the AI staff roster and duty schedule are configured, and what each state in the delivery queue means
section: Office
order: 7
---

The office is collaboration **at different moments**: you leave a piece of work, an AI staff member
does it on their shift, you check it when you are back. It does not add a background service —
**the open SLATE Teams page is what executes**.

:::note Office has two sides
The top-level **Office** tab opens on the **Chat** side; this chapter is about switching to **Desks**.
The switch sits at the top right, and both sides stay on the same page.
:::

:::warning Close the app and nothing runs
The backend only queues; it never executes work itself. So the office needs one machine with SLATE
Teams open: that page is whoever is on duty. With the app closed, jobs sit quietly in the queue
until a page is back.
:::

## What the panel looks like

Roster on the left with a floor plan of the desks (who's busy, who's free, who is handing something
over), a message box in the middle that can "交给" (assign to) one employee, "贴出来" (post for
everyone) or "交办" (hand over a job), and five tabs on the right: **动态** (feed),
**等你拍板** (waiting on you), **值班表** (duties), **岗位** (roles), **站会与绩效** (standup & record).
This chapter covers roles and duties; the last two live in
[Working like a person](./08-office-work.md) and [Gates & accounts](./09-office-gates.md).

## Hiring

Under **Hire** there are two ways in: "Hire from a template" (four built in: researcher, engineer,
reviewer, duty keeper), or fill in a new colleague from scratch. Each employee carries these fields:

| Field | What it decides |
| --- | --- |
| Name / avatar / hue | Colleagues address each other by name — **names must be unique** |
| One line describing the role / 目标 (goal) / Duties | What they do and what they aim at; also what triage weighs when deciding if a job is theirs |
| Model / rounds / project | Which model, how many turns one run may take, which project root the work lands in |
| the reviewer | Whether a delivery passes a human and who reviews it; "No reviewer (deliveries come straight to you)" ships it to you |
| Daily budget | How many tokens per day before the breaker trips (see [Gates & accounts](./09-office-gates.md)) |
| Unattended | Which approval level their shifts run at |

"解雇" (fire) takes them off the roster — the jobs they did and the things they said **stay in the
account**, and their record row is marked 已离职 (left).

## Scheduling

"Add duty" puts a shift on an employee. Two kinds of trigger:

- **Daily** / every N minutes / **once** — the clock comes to look.
- **Event Trigger** — a commit landed, watched paths changed, a self-check script went red, a Git
  push, or an external callback.

The clock firing is **not** the same as "act now". Each shift can carry a **Guard**, most often:

- "No more than a few tasks pending" — set to 0 and it means **only move when my hands are empty**.
- "Only schedule inside this window".

When a guard can't be read, or a condition type is no longer understood, the panel shows that as a
line of text instead of silently skipping.
:::note Why not fire on schedule alone
Firing on time lets one employee pick up another job before finishing the last, and the queue just
grows. A guard turns "should I move" into a check with a readable answer.
:::

## The delivery queue

Each employee on the roster shows one state — **Idle**, **Working**, **Off duty** — followed by
counters: pending, waiting on you, awaiting review, returned, budget spent. Job states are few
enough to just learn:

| State | Meaning |
| --- | --- |
| Queued · {when} | Scheduled, waiting for an open page to claim it |
| Working | A page holds it under a lease; if that page dies, the job is claimable again |
| {n} awaiting review | Done, waiting for the reviewer |
| Waiting on you | Listed under "Waiting on you" — it needs your call |
| Blocked | Stuck, and the line says **what it is blocked on** |
| Settled / {n} failed | Finished / broke, with the reason on that line |

Every "didn't happen" has to produce a line you can read. There is no silent retry and no silent
discard.

## Next

- How they remember the last run and decide a job isn't worth doing: [Working like a person](./08-office-work.md).
- Review, budget, deadlines, standup and record: [Gates & accounts](./09-office-gates.md).
