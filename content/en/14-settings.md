---
title: Settings
description: What the 21 groups in the settings sidebar each cover, with the detail on models and context, custom theme, and AI-assisted features
section: Data & settings
order: 14
---

Settings is the sixth tab in the top bar. The left column is an anchor navigation with a search box above it; the right
column holds the grouped blocks. **The navigation is read from the blocks at runtime**, so the group count follows the
version while the order always matches the main area. There are **21 groups**: Models · API test · Usage · Context &
project · Auto-advance · AI-assisted features · Notifications · Background tasks · Parallel runs & projects · Minimal UI
(experimental) · Custom theme · Web search · Image generation · Video generation · Approval mode · Backup & restore ·
Session archive · Storage · LAN remote control · Typing game · About.

Press **Save** at the top right to write everything. Interface language is **not here**: it is chosen at install time
(written to `data/language.txt`) and never switched inside the app, with precedence `SLATE_LANG` > that file > Chinese.

## Models and context

**Models** does two jobs: custom models (name/ID, request style — OpenAI-compatible, Anthropic, or raw curl — Base URL,
API Key, context window) and the keys for built-in models, plus an optional Responses API switch. **API test** fires one
minimal request down the real chain — the same one a conversation uses, not a parallel one.

**Context & project** decides how much a model can see at once. Built-in models and models with a declared window run on
"auto", each taking eighty percent of its nominal window, so the global cap here is only a backstop for models with no
window information; to tune one model, use the "max context" control on its row in Models — the slider is a rough pick,
the number box beside it takes an exact value, and local or custom endpoints can **probe the window**. The compression
threshold and the context meter compute from that same number. Then: a single-output cap of 1024–65536, with
"Raises the output length limit to 65536 when writing files so large files are not truncated" on by default;
"auto-confirm file creation and modification"
on by default, and off it returns to preview-then-accept for every write; and the **project constitution** — standing
hard rules for this project, with the prompt factory entry point in the same group.

## Custom theme

With a custom theme enabled you fill in **only four source colours** (page background, panel, body text, accent); every
other value is derived from them by luminance and contrast, so body text and the three secondary levels are pulled up to
readable. The preset palette has **10 tiers**: paper, ink night, mist blue, deep sea, pine, moss, clay, dusk plum, graphite,
letterpress. A preset fills the four swatches and each stays editable — but **once edited, the theme belongs to no preset**.

:::warning Light/dark is locked while it's on
With a custom theme active, the top-bar light/dark button and Ctrl+D do nothing; pressing one tells you why. Switching
the custom theme off returns the whole look to the built-in theme.
:::

- **Fonts**: families installed on the system are used by name. "Import font" takes one `.woff2 / .woff / .ttf / .otf` file
  up to 16MB and it lands **only on this machine, under `data/theme/fonts/`** — not in conversation records, not in the
  repository, not in the installer, and it does not travel to another machine with a backup; with one weight imported,
  the browser fakes bold and italic.
- **Panel opacity** (55%–100%) is a **flat alpha** on the panel, card, input and assistant-bubble layer: lowering it
  reveals the page colour or your wallpaper behind it, and **it is not frosted-glass blur**. Your own bubbles and code
  blocks always stay solid.
- **Background image** is stored on this machine under `data/theme/`, with a veil slider (40%–95%) — too low and body
  text sits on the picture, too high and the picture might as well not be there. The Wallpaper Engine row only reads that
  app's own configuration and preview image and uses it as your background; it does not start the app or change its
  settings.

## AI-assisted features

Every feature that calls a model **on its own** — apart from conversation, team debate and the prompt factory — is in
this group: **15 items**, each with its own switch, and **12 of them** can pick their own model. The other three carry no
model picker because ownership differs: scheduled and event tasks choose a model **inside each task**; image and video
generation are configured in their own blocks. **Switch an item off and no request is made for it again.** The twelve are
context compression summary, memory auto-distillation, manual memory extraction, conversation insight capture, automatic
session title, code understanding document, code review, board AI organize, prompt polish, sub-agent parallelism,
dangerous-command purpose explanation and team workflow execution. (The Auto-advance reviewer model and the
background-task auto-resume are set in their own groups, not repeated here.)

## Why capability management isn't here

Tools, skills, reply modes, expert packs, MCP servers and Actions all live on the [Extensions](./11-extensions.md) tab —
the **single source of truth** for the capability list. Settings keeps two kinds of thing: **provider configuration** for
capabilities (the web-search engine and rendering mode, the image/video model and key) and the **call gate** (those 15
switches above). Each half of one concern stays in exactly one place.

:::note Approval mode is here, reply mode is not
This page sets the default **approval mode** for new conversations (manual / auto / full access / night). A **reply
mode** is [a different thing](./11-extensions.md), chosen per conversation above the input box.
:::

## Data and devices

**Backup & restore** exports one JSON (conversations, debates and the ledger, the staff roster and duty schedule, memories,
assets, settings); restore merges by id and never overwrites what is there — [Projects & data](./12-projects-data.md).
**Session archive** holds archived sessions, restorable or deletable for good; **Storage** compacts the database and clears
caches; **LAN remote control** serves this machine's address to a phone or tablet — see [Mobile](./13-mobile.md).
