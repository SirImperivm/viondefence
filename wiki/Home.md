# VionDefence Wiki

**English** · [Italiano](IT-Home)

Step-by-step guides for setting up and running VionDefence on your Discord server.

> Looking for the exhaustive reference — every command option, every setting, every
> default? That lives in the [reference documentation](https://github.com/SirImperivm/viondefence/tree/master/docs).
> This wiki is the walkthrough; the docs are the manual.

---

## Start here

| Page | What you'll do |
|---|---|
| **[Getting started](Getting-Started)** | Understand what VionDefence does and what you need before you begin |
| **[Installation](Installation)** | Invite the bot, grant the right permissions, open the dashboard |

## Configure the sections

Everything is configured from the dashboard at
[viondefence.com/dashboard](https://viondefence.com/dashboard). One page here per
section of the sidebar.

| Section | Page | Configure it when you want… |
|---|---|---|
| Generale | **[General](Configuration-General)** | The bot's language, timezone and date format |
| Comandi | **[Commands](Configuration-Commands)** | To control who can run which slash command |
| Canali template / privati | **[Voice channels](Configuration-Voice-Channels)** | Members to get their own voice rooms on demand |
| Ticket | **[Tickets](Configuration-Tickets)** | A support ticket system with panels and transcripts |
| Moderazione | **[Moderation](Configuration-Moderation)** | Sanctions, DM notices, warn escalation, embed colors |
| Automod | **[Automod](Configuration-Automod)** | Automatic filtering of spam, links and insults |
| Log | **[Logs](Configuration-Logs)** | A written record of everything the bot does |
| Contatori | **[Counters](Configuration-Counters)** | Live member, bot and staff counts shown as channels |
| Livelli | **[Levels](Configuration-Levels)** | Members to earn XP and climb levels for taking part |
| Bump ME | **[Bump ME](Configuration-Bump)** | To advertise your server in the bot's own description |

---

## The 10-minute setup

If you just want a server that works, do these in order and stop:

1. [Install the bot](Installation) and open the dashboard.
2. [General](Configuration-General) — set language, timezone, date format.
3. [Logs](Configuration-Logs) — point at least **Moderation** and **General** at a
   staff-only channel. Without this you are configuring blind.
4. [Moderation](Configuration-Moderation) — set the mute role.
5. [Commands](Configuration-Commands) — check the default permissions match your staff
   roles.

Everything else is optional and can wait until you need it.

---

## Getting help

- Discord support server and contact email: https://viondefence.com/contacts
- Something wrong in this wiki? Open an issue on the
  [repository](https://github.com/SirImperivm/viondefence/issues).
