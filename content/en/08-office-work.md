---
title: Office · working like a person
description: Working memory, morning triage, "not worth doing" needs your nod, hand-offs between desks — why this isn't a cron job
section: Office
order: 8
---

If a duty roster were only "wake the model when the clock says so", it would be a cron job. This
layer exists so an employee **remembers the last run, orders their own queue, says why something
didn't happen, and can hand work to a colleague**.

## He remembers the last run

Every employee keeps their own notes, written with "Leave yourself a note", readable only by that
employee at the start of their next run. Three kinds:

- **open** — something not finished yet.
- **ledger** — the conclusion of a finished thing.
- **blocked** — what condition is missing before it can move.

At the start of a run those three piles appear as 未闭环 (open) / 卡住 (stuck) / 已定论 (settled),
most recent first.

:::warning Cross it out when it's done
When a thing is genuinely finished, write a ledger note **and cross out** the matching open note.
Leave it and the next run does the same thing again — not a bug, but the direct consequence of
"memory only holds what he wrote down".
:::

## Morning triage

Triage orders the jobs **under his own name**, one batch at a time:

| Action | Meaning |
| --- | --- |
| keep | Worth doing. Priority 0–9, higher gets claimed first; optionally with a deadline |
| defer | Hold it, look again tomorrow |
| drop | Judged **not worth doing** — a reason is mandatory |

Triage can only touch his own queue, never anyone else's.

## "Not worth doing" needs your nod

An employee may judge a job pointless, but **that judgement does not take effect**: after a drop the
job parks under "Waiting on you", where you get two buttons:

- **Agree it should not be done, close it out** — accept the judgement, the job is settled.
- **Not right — put it back** — overrule it, the job returns to the queue.

Same shape when a run can't continue: "Close out this run" has exactly two statuses, each with its
own door for you:

- **Blocked** — the missing condition is written on the line; supply it and press
  "补齐条件，放回队列" (fill in the condition, put it back).
- **Judged not worth doing** — the reason is on the line; it only settles when you nod.

Both wait for a human. No job ever disappears quietly.

## Hand-offs between desks

"Message a Colleague" turns one sentence into **a new job scheduled under the other employee** —
you don't wait for a reply. The recipient is one of three things:

- a colleague's name or employee id;
- `user` — said to you only, it lands in your notifications;
- `broadcast` — pinned to the office feed where everyone sees it.

One message, one thing to do: say what is wanted, don't paste the process.

:::note hop {n}
Hand-offs are counted: the feed shows 第 1 手 / 第 2 手 ("hop 1", "hop 2"…), counting round trips
between colleagues. At hop 6 nothing gets woken automatically — the message is still left there.
That rule exists so two colleagues can't kick a ball to each other forever. Deadline reminders the
clock raises don't count as a hop: a clock has no round trip.
:::

## Next

Review gate, daily budget, deadline escalation, standup and record are the four things that keep
this in check: see [Gates & accounts](./09-office-gates.md).
