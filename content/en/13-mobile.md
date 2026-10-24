---
title: Phone remote control
description: What the phone screen has and doesn't have, where the remote-control switch lives, and what headless mode is for
section: Data & settings
order: 13
---

Remote control is **the same backend with a different face**: your phone's browser talks to the
backend on your machine and drives the same engine — no second service, no second way of executing.

## What the phone has

Five tabs: **Chat**, **Chats** (the session list), **Memory**, **Tasks**, **Settings**.

- Streaming replies, collapsed reasoning and tool cards all work; tools really touch files (create,
  edit and append go through the same endpoints as on the desktop).
- Approval became a bottom sheet: risky commands and file changes still need your nod, with a diff preview before anything lands.
- Settings holds four things: the remote-control address with its QR code, model choice, keys, theme.
  Background-task events are read back into a finished pass as usual.

## What the phone doesn't have

The **Team**, **Office**, **Board** and **Extensions** tabs exist on the desktop only. So:

- You can't open a debate from a phone and can't see the delivery queue. A participant holding a
  ticket lands on another page entirely — that discussion and nothing else.
- A phone page **never claims office work**. The backend only queues; the one on duty is the desktop
  page that is open, so with only a phone online an AI staff member's jobs sit quietly in the
  [delivery queue](./07-office.md).

:::warning A phone is a remote, not a second machine
Files, Git, terminals and the ledger live on the host; put the host to sleep and nobody is working
on the other end of that link.
:::

## How you get the phone screen

Open the address with its auth code on a phone and the page routes itself to the touch layout,
keeping the code in the URL. Add `slate_mobile=0` to stay on the desktop layout.

## Where the switch lives

**Settings → LAN remote control → enable**, and that is the only place.

- The preference lives in `data/desktop_state.json`. A missing file, a broken read or a missing key
  all mean **on** — defaulting to off would leave existing installs suddenly unreachable.
- Turning it off **really releases the listening port**; it doesn't just hide the address.
- The switch is **host-only**. Flipping it from a device on the remote port is refused: that device
  is working through the very connection it would cut.

## How to get the address

The settings block on the host lists the address with its auth code — copy it or scan the QR code.
It is built from this machine's LAN IP and the port the side service **actually got**: it prefers one
port and walks upward when that is taken, so don't hard-code the number anywhere else.

:::note Re-copy the address after a restart
The master auth code is generated fresh for every process, so a restart invalidates old links; a
phone stuck on "authorization required" just needs a freshly copied address.
:::

## Headless mode

```
python desktop.py --remote
```

For machines with no desktop environment (a server, a Raspberry Pi, a container): no window, no
tray — just the backend plus LAN remote control, with the local address and the authorized remote
address printed to the terminal; Ctrl+C shuts it down. It forces remote control on **for this
process** without writing the preference, and refuses to reuse a backend someone else started,
because headless leaves no window to fix things with. A failed backend reports itself in the terminal.

## Why only the face changes

The tool loop, message assembly, approval decisions and rendering logic all sit in the shared service
modules; the phone injects only its own view and input. One engine behind two faces, so you never get
"it looked doable on the phone but ran something else". The trade-off is honest too: debate and office
interaction doesn't fit a touchscreen, so it isn't ported.

## Next

- Tickets and the narrowed scope behind them: [Team · the debate hall](./06-team.md).
- Why work waits for an open page: [Office](./07-office.md).
- Switches a backup doesn't carry: [Projects, backups and the ledger](./12-projects-data.md).
