---
title: Install & launch
description: Three ways to install (Windows, macOS, source), configuring your first model, and how ports split when SLATE is on the same machine
section: Start
order: 2
---

## Install

### Windows

Download `SLATE-Teams-Setup-<version>.exe`, run it, and launch from the desktop icon. It installs
into `AppData\Local\Programs\SLATE Teams` for the current user and needs no administrator rights.

The first launch opens a local window — that's the [six tabs](./03-interface.md).

### macOS

Releases ship `SLATE Teams.app` and `SLATE-Teams-Setup-<version>.dmg`. From source, package it with
`build_macos.sh` in the repository, or just run `python desktop.py` (see "From source" below).
The installed app keeps its data in `~/Library/Application Support/SLATE Teams`, not inside the
bundle.

:::note Blocked the first time you open it
An unsigned build gets stopped by Gatekeeper once. Choose "Open Anyway" under
System Settings → Privacy & Security; you only do this once.
:::

### From source

```
git clone <repo url>
cd SLATE_Teams
pip install -r requirements.txt
python desktop.py
```

`desktop.py` starts the backend and opens the window itself. If you only want the API for another
browser, run `python backend/main.py` and open `http://127.0.0.1:<port>/`.

## Configure your first model

Settings → 模型/上下文 (models & context): fill in one provider's API key, pick a default model,
and you're running. The key is written only into the local `data/desktop_state.json`; it never
appears in an outbound request and never enters a backup.

:::warning Your keys are not in the backup
Exports contain no model keys and no local preferences. After restoring on another machine you fill
the keys in again — deliberately.
:::

## Coexisting with SLATE

The two products can sit on one machine without overwriting each other:

| | App port | Data |
| --- | --- | --- |
| SLATE | its own default | `data/` inside its own install |
| SLATE Teams | 8130 preferred, moves on if taken | `data/` inside its own install |

Installer identity, Start Menu entries and update feeds are all separate, so installing Teams can't
hijack SLATE's auto-updates.

## If it won't start

1. **Port taken**: `desktop_backend.log` in the data directory prints the port it actually got.
2. **Missing dependencies**: most common when running from source; the error names the package.

More in [FAQ](./15-faq.md).
