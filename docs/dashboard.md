# The dashboard

**English** · [Italiano](it/dashboard.md)

Everything VionDefence does is configured from the web dashboard at
https://viondefence.com/dashboard. The slash commands are a convenience layer on top of
the same settings.

---

## Getting in

Log in with Discord. The server picker lists every server where **both** are true:

- you have the **Manage Server** permission, and
- VionDefence is installed.

Pick one to open its configuration. Changes take effect immediately — there is no
separate deploy step, and no need to restart anything.

---

## Sections

### General

Language, timezone, date format and time format for the server.

The **language** here is the language of the messages the bot sends *in that server*.
It is independent of the language of the dashboard itself, which follows your own
preference.

Available: English (`en-US`) and Italiano (`it-IT`).

### Commands

One row per slash command, with four controls each: **enabled**, **required
permission**, **allowed roles**, **allowed channels**.

Full reference and defaults: [Commands](commands.md#permissions-and-restrictions).

### Templated channels

Voice channel templates — hub channel, destination category, name format and user
limit. See [Voice channels](voice-channels.md#templated-channels).

### Private channels

The personal-room system — on/off, hub channel, category.
See [Voice channels](voice-channels.md#private-channels).

### Tickets

Ticket panels: categories, teams, forms, transcripts.
See [Tickets](tickets.md).

### Moderation

The mute role, per-sanction DM notifications, warn expiry and the warn escalation
rules. See [Moderation](moderation.md).

### Logs

Destination channel, embed color and thumbnail for each of the nine log categories.
See [Logs](logs.md).

### Automod

The three automod modules, their thresholds and their action modes, plus the shared
exemption lists. See [Automod](automod.md).

### Content filter

Per-channel rules on **what kinds of content may be sent**: text, files, images and
links. Channels you do not list keep accepting everything.

Each filtered channel gets its own combination — a channel can allow files and images
but not plain text, or allow text and images but not links, and so on.

Text attached to a file or an image is treated as a **caption**: it stays allowed even
when text itself is filtered out, as long as it fits within **1024 characters**.

Threads inherit the filter of the channel they were started from. Exempt roles and
exempt members are never filtered and, while *respect the role hierarchy* is on,
neither is the server owner nor anyone above the bot.

A blocked message is simply **deleted**, and its author gets a **direct message**
explaining what that channel allows. The content filter never warns, mutes, kicks or
bans anyone — the removal is only written to the **Content filter** log category.
The DM can be turned off, in which case the message is removed silently.

Requires the **Pro** plan.

### History

Every sanction ever issued on the server, filterable. From here you can:

- open a **sanction detail** page — moderator, target, timestamps, reason, status,
  and the revoke action;
- open a **member profile** — everything that member has collected in one place.

Also shows automod logs, so you can audit what the filters caught.

---

## Account

Outside the per-server dashboard, the **Account** area covers you rather than a server:

- **Personal** — your profile details.
- **Access** — email, password, and the link between your account and Discord.
- **Subscriptions** — your active plans and their servers.

You can sign in with Discord, or with an email and password, and link the two so
either works.

---

## Plans

Some features and some limits — how many channel templates, how many ticket panels,
which log categories — depend on the plan attached to a server.

Current plans and what each includes: https://viondefence.com/pricing

A plan is assigned to a specific server. Changing which server a plan covers, or
changing plan, is done from **Account → Subscriptions**.

---

Next: [Commands](commands.md)
