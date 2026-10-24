---
title: Models & usage
description: Where the model registry lives and which vendor prefixes to know, where keys are stored and whether backups carry them, how the context budget is computed and how to read the usage strip
section: Daily
order: 4
---

## Where models come from

The built-in list lives in the backend registry (`backend/routers/proxy.py`). The frontend fetches it at startup,
in three groups: **International models**, **Chinese Models**, **Local models**.

Recognising a vendor by its id prefix is enough: `gpt-`, `claude-`, `gemini-`, `deepseek-`, `kimi-`, `qwen-`,
`glm-`, `doubao-`, `MiniMax-`, `ernie-`; the local entry is simply id `local` (Ollama / LM Studio). Each vendor's
request URL and declared context window are written in the registry — you never fill them.

:::note Reasoning levels differ per vendor
Some can be switched off, some force thinking (Kimi K3 and GLM-5.3 have no "off"), some only offer a bare toggle.
The "Reasoning effort" control therefore shows a different set of stops per model.
:::

## Where keys are stored

Settings → Model Config → "Built-in Model Keys", one key per vendor; the **Keys** button in the topbar opens
Settings directly. When you send, the local backend takes the key and authenticates against that vendor. Keys land
in `data/desktop_state.json` under `modelKeys`, with a copy in the browser's local state. The LAN remote reads that
same file, so configuring it once covers the phone too.

:::warning Backups **do** contain your keys
Settings says it plainly: a backup is "a single JSON file containing the backend database and local settings".
Local settings include `modelKeys`. **Treat the backup file as a secret** — no group chats, no public cloud drive,
never commit it to a repository.
:::

## The context budget

The denominator of that percentage is not the model's declared window — it is **this session's budget**:

- **"Auto"** (the default) = the model's declared window × **0.8**, floored, **not snapped to a slider stop**.
- Only models with no window information at all fall back to the global "Context Token Limit" (64000 by default).
- A value you set by hand wins, but never above that model's declared window.

The 20% is for output. Snapping to whole stops would flatten 128K / 200K / 256K into one number, and a small-window
model can't reach the lowest stop at all — it would return 0 and occupy the full window with no room left to answer.

The same budget feeds two places: where the context bar counts as full, and which round auto-compaction fires on.
One number, so "it compacted while still under the limit" cannot happen.

To tune one model: "Max context" on its row in Model Config — the slider rough-selects, the number box takes an exact
value, and local or custom endpoints can "Probe window" to ask the endpoint itself. When budget and declared window
disagree, the usage strip's hover shows both numbers.

## How to read the usage strip

The strip above the conversation, left to right:

| Segment | What it is |
| --- | --- |
| Model name | The current model; a warning mark appears beside it when no key is set |
| Messages | Message count for this conversation |
| In | Cumulative prompt tokens |
| Out | Cumulative completion tokens |
| Total | The two summed |
| Context | Tokens in use, plus a progress bar for the share of budget |

The Context segment is clickable and jumps to that model's budget slider in Settings. Hovering the strip expands
**Context Breakdown** into five buckets: System Prompt / Tool Catalog / Skill Injection / Tool Calls & Results /
Messages, each with its share.

:::note These are estimates
Tokens are estimated at roughly 3 characters per token. Trust the share and the trend, not a line-by-line match
with your upstream bill.
:::

## Switching models and adding a vendor

- **Switch model**: the model dropdown in the chat input toolbar. It is one global setting — changing conversation
  does not change the model, though each conversation keeps its own usage counters.
- **Add a vendor**: Settings → Model Config → "+ Add Model". Three request modes: OpenAI-compatible (appends
  `/chat/completions` itself), Anthropic (`/v1/messages` + `x-api-key`), or raw curl (Base URL is the full endpoint).
  Then fill Base URL, API Key (optional) and Context Window.
- **Backup & restore**: Settings → Data Backup & Restore merges by id and does not overwrite existing data. Details
  in [Projects & data](./12-projects-data.md).
