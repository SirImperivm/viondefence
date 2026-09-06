# Getting started

**English** · [Italiano](it/primi-passi.md)

Three steps and about two minutes to get VionDefence running on your server.

---

## 1. Add the bot to your server

Use the **Add the bot** button on the [website](https://viondefence.com) and pick the
server you want to install it on.

You need the **Manage Server** permission on that server — Discord only lists servers
where you have it.

During the invite, keep the permissions Discord suggests. VionDefence needs them to
do its job:

| Permission | Used for |
|---|---|
| Manage Channels | Creating and deleting temporary voice channels and ticket channels |
| Manage Roles | Applying the mute role, ticket channel permission overwrites |
| Kick Members / Ban Members | `/kick`, `/ban`, automod active actions |
| Moderate Members | `/timeout` and automod timeouts |
| Move Members | Moving members into their new temporary voice channel |
| Read Message History / Send Messages / Embed Links | Log embeds, ticket panels, transcripts |

> If you remove one of these permissions later, the related feature stops working
> silently from the member's point of view — the failure is reported in the
> **General** log category instead. See [Logs](logs.md).

---

## 2. Open the dashboard

Go to https://viondefence.com/dashboard and log in with Discord.

You will see every server where you have **Manage Server** and where VionDefence is
installed. Click one to open its configuration panel.

If a server is missing from the list:

- the bot is not installed on it, or
- you do not have Manage Server on it, or
- your Discord session is stale — log out and back in.

---

## 3. Set the basics

Open the **General** section first and set:

- **Language** — `English (en-US)` or `Italiano (it-IT)`. This is the language of every
  message the bot sends *in that server*, independently of your dashboard language.
- **Timezone** — used for every timestamp in logs, transcripts and history
  (e.g. `Europe/Rome`).
- **Date format** and **Time format** — how those timestamps are rendered
  (e.g. `DD/MM/YYYY` and `HH:mm:ss`).

Defaults are `en-US`, `America/New_York`, `MM/DD/YYYY`, `hh:mm:ss A`.

---

## 4. Then configure what you actually need

Nothing else is enabled by default. Pick the modules you want:

| I want… | Go to | Guide |
|---|---|---|
| A log of what the bot does | **Logs** | [Logs](logs.md) |
| Kick/ban/warn/mute with history | **Moderation** | [Moderation](moderation.md) |
| Automatic spam / link / insult filtering | **Automod** | [Automod](automod.md) |
| Members to get their own voice room | **Templated channels** | [Voice channels](voice-channels.md) |
| A support ticket system | **Tickets** | [Tickets](tickets.md) |
| To restrict who can run which command | **Commands** | [Commands](commands.md#permissions-and-restrictions) |

A sensible order for a fresh server is: **General → Logs → Moderation → Commands**,
then the optional modules.

---

## A note on the mute role

`/mute` and the automod `mute` action both need a **mute role** configured in
**Moderation**. Until you set one, those actions fail.

Create a role in Discord (e.g. `Muted`), deny it *Send Messages*, *Speak* and *Add
Reactions* in your channels, then select it in the dashboard. Make sure the
VionDefence role sits **above** it in the role list, otherwise the bot cannot assign it.

---

Next: [Dashboard](dashboard.md)
