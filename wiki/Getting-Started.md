# Getting started

**English** · [Italiano](IT-Primi-Passi)

Before you invite anything, five minutes of context so the rest of the wiki makes sense.

---

## What VionDefence is

A Discord bot that handles moderation, tickets, temporary voice channels and automatic
content filtering — configured from a **web dashboard** rather than from a long list of
slash commands.

The slash commands still exist, and staff use them day to day. But the setup happens in
the browser, and nothing in the bot has to be re-taught to your team through command
syntax.

---

## What you need

| Requirement | Why |
|---|---|
| A Discord server | Obviously |
| **Manage Server** on it | Discord only lets you install bots where you hold it, and the dashboard only lists servers where you hold it |
| A few minutes | The base setup is genuinely short |

You do **not** need a database, a host, or any technical setup. VionDefence is a
hosted service.

---

## How the pieces fit together

```
Discord server  ──►  VionDefence bot  ──►  logs, sanctions, tickets, voice rooms
       ▲                     ▲
       │                     │
   your members         you, from the
   using commands         dashboard
```

Three things are worth understanding up front:

**1. Configuration is per server.** Every setting you will read about lives on one
Discord server. If you run three servers, you configure three times. The plan attached
to a server is likewise per server.

**2. The bot's language is separate from yours.** The dashboard follows your personal
preference. The language the bot *speaks in a server* is a server setting. An Italian
admin can perfectly well run an English-speaking server.

**3. Nothing is enabled by default.** Fresh out of the box, no log category has a
channel, no automod module is on, no voice template exists, and there is no mute role.
This is deliberate — the bot does not touch your server until you tell it to. The one
exception is the slash commands, which are active from the start with sensible
permission defaults.

---

## The order that works

Setting things up in this order avoids the two most common frustrations — configuring
blind, and mutes that silently fail:

1. **[Install the bot](Installation)** and open the dashboard.
2. **[General](Configuration-General)** — language, timezone, date format. Do this
   first: every timestamp you see afterwards depends on it.
3. **[Logs](Configuration-Logs)** — give at least *Moderation* and *General* a channel.
   Now you can see what the bot is doing and why something failed.
4. **[Moderation](Configuration-Moderation)** — the mute role, and the role hierarchy
   that makes it work.
5. **[Commands](Configuration-Commands)** — confirm the permission defaults line up with
   your staff roles.

Then, whenever you actually want them:

- **[Voice channels](Configuration-Voice-Channels)** — on-demand voice rooms.
- **[Tickets](Configuration-Tickets)** — the support system.
- **[Automod](Configuration-Automod)** — automatic filtering. Read the page before
  turning anything on; there is a right way to roll it out.

---

## A word about permissions

Most "the bot isn't working" reports come down to one of three things:

- a **Discord permission** the bot is missing;
- the **role hierarchy** — the bot cannot act on anyone ranked above it, and cannot
  assign a role that sits above its own;
- a **log channel** that was never set, so the failure is invisible.

The [Installation](Installation) page covers the first two properly. Set the logs early
and the third stops being a problem.

---

Next: **[Installation](Installation)**
