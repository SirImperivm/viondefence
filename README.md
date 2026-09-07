# VionDefence

**English** · [Italiano](docs/it/README.md)

**VionDefence** is a Discord bot for server owners who want moderation, tickets,
temporary voice channels, automod and an XP level system in one place — configured
from a web dashboard instead of a wall of slash commands.

> This repository contains the **public documentation only**. The bot and website
> source code are not published here.

- **Website:** https://viondefence.com
- **Dashboard:** https://viondefence.com/dashboard

---

## Documentation

New here? Start with the **[Wiki](https://github.com/SirImperivm/viondefence/wiki)** — step-by-step setup guides in English and
Italian. The pages below are the full reference.

| Guide | What's inside |
|---|---|
| [Getting started](docs/getting-started.md) | Invite the bot, log in, first configuration |
| [Dashboard](docs/dashboard.md) | Every panel of the web dashboard, explained |
| [Commands](docs/commands.md) | Full slash command reference |
| [Moderation](docs/moderation.md) | Sanctions, durations, warn escalation, history |
| [Automod](docs/automod.md) | Anti-flood, anti-advertising, anti-insult |
| [Member counters](docs/counters.md) | Live member, bot and staff counts as channels |
| [Level system](docs/levels.md) | XP, the level curve, rewards, leaderboard |
| [Bump ME](docs/bump.md) | Sponsor your server in the bot description |
| [Temporary voice channels](docs/voice-channels.md) | Channel templates and private rooms |
| [Tickets](docs/tickets.md) | Panels, forms, teams, transcripts |
| [Logs](docs/logs.md) | Log categories and channel routing |
| [FAQ & troubleshooting](docs/faq.md) | Common problems and their fixes |

---

## What VionDefence does

**Moderation** — kick, ban, mute, timeout and warn, all with optional durations,
optional DM notifications to the sanctioned member, and a full searchable history
per member and per staff member.

**Automod** — three modules (anti-flood, anti-advertising, anti-insult) that can
either just log a violation or automatically apply a sanction, with role and user
exemptions.

**Temporary voice channels** — members join a hub channel and get their own voice
room, created from a template and deleted the moment it empties. Owners control
their room (name, user limit, privacy, trust/kick/ban) from a button panel or the
`/voice` command.

**Tickets** — configurable ticket panels with custom open forms, separate
user/support/admin teams, claim and release, and HTML transcripts on close.

**Member counters** — voice channels nobody can join that show how many members, bots
and staff the server has, refreshed on their own. `/server stats` adds how many of them
are online right now.

**Levels** — members earn XP by writing and by sitting in voice, on the channels you
choose. The cost of each level is a formula you write, and each level can hand out a
role or a written reward. `/level` and `/userinfo` show where anyone stands.

**Bump ME** — `/bump` puts your server name and invite into the bot's own Discord
description for 12 to 24 hours, one server at a time across the whole bot.

**Logging** — eleven independent log categories, each with its own destination
channel, embed color and thumbnail.

**Localization** — the bot and the dashboard are available in English (`en-US`)
and Italian (`it-IT`); the language is set per server.

---

## Quick start

1. Invite VionDefence to your server (you need **Manage Server** on it).
2. Go to the [dashboard](https://viondefence.com/dashboard) and log in with Discord.
3. Pick your server and open **General** to set language, timezone and date format.
4. Configure the modules you need — see [Getting started](docs/getting-started.md).

---

## Support

- Discord support server and contact email: https://viondefence.com/contacts
- Terms, privacy and billing: https://viondefence.com/terms

---

*VionDefence is not affiliated with Discord Inc.*
