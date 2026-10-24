---
title: Office · gates & accounts
description: The review gate, the daily token budget, deadline escalation, and where the standup and record cards get their numbers
section: Office
order: 9
---

Handing work to AI staff needs a few gates: deliveries shouldn't land on you unexamined, spend has
to have a ceiling, and an expired deadline shouldn't rot on the desk. All four live in this layer,
and every number is computed from **the same jobs table** — there is no second ledger.

## The review gate

When you hire someone you pick "the reviewer" for them. Their deliveries go to that reviewer first
and **not straight to you**.

- Review is itself **a job scheduled under the reviewer**: it shouldn't sit behind ordinary duty
  work, so it queues slightly ahead — but anything triage raised above it still goes first. Its
  deadline defaults to two hours.
- The reviewer closes it with "Judge This Delivery", and there are exactly two verdicts:
  **approve** (it passes, and this is the first time the delivery reaches you) or **return**
  (it fails, back to the author, with what to change written down).
- The reviewer must exist in the roster, **cannot review themselves**, and cannot review for
  someone who has left the roster.

:::note The wording you see differs
Before review passes you only get "An employee sent a delivery for review"; after it passes you get
"Employee delivery". When it comes back the line reads "Returned in review: why". That split is
deliberate — **something that hasn't passed shouldn't look like a delivery**.
:::

A returned job is re-done through the same [hand-off](./08-office-work.md) channel, so it counts in
"hop {n}" too and stops at hop 6.

## Daily budget

Each employee can carry a **Daily budget** in tokens. Once today's spend reaches it:

- the duty roster **schedules no new work**, and the job shows up as **Blocked** with the reason on
  the line;
- **morning triage and your own "Run now" still schedule**. Otherwise a full budget would lock you
  out of even asking them to finish the last item in hand.

The record column reads "{used today} / cap {budget}" and marks **Budget spent** once it's over.

## Expired deadlines escalate to a human

If triage gave a job a deadline, the clock speaks for the human once it passes: a system line
appears in the feed and the job moves into "Waiting on you". The same reminder fires **once** —
refreshing doesn't nag you again — and each pass escalates only a handful of jobs, because flooding
the feed is the same as not reminding anyone.

## Two cards

**Today's standup** — every shift that had "Morning triage" checked leaves one self-reported line:
who, what they said, when. If nobody has reported it says so and tells you to put a triage shift on
someone, rather than showing you an empty table.

**Record** — one row per employee: {n} done, {n} failed, {n} waiting on you, {n} awaiting review,
{n} returned, how long a run takes on average, and how many tokens went today.

:::warning What "average" measures
That column spans **claim to close-out**, not end-to-end wall clock — time spent waiting in the
queue isn't counted. It's an order of magnitude, not a receipt.
:::

## Next

How these jobs, messages and verdicts get into a backup: [Projects & data](./12-projects-data.md).
