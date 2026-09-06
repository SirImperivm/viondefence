# Configuration — Logs

**English** · [Italiano](IT-Configurazione-Log)

*Dashboard → your server → **Log***

Set this up early. Logs are how you find out that a permission is missing, that a mute
failed, or that automod caught something it should not have.

---

## How the section works

You get one card per log category. Click the **wrench** on a card to open its editor —
a popup form with three fields:

| Field | What it does |
|---|---|
| **Channel** | Pick the destination from the list of the server's text channels. Selecting *Disabled* turns the category off |
| **Embed color** | The colored bar down the left side of the embed |
| **Thumbnail URL** | Optional small image in the embed's corner |

Leaving a category on **Disabled** is how you switch it off. Nothing is sent and nothing
errors.

---

## The eight categories

| Category | What lands here |
|---|---|
| **General** | Server-level events, and bot errors that do not belong anywhere else |
| **Commands** | Command usage |
| **Moderation** | Kicks, bans, mutes, timeouts, warns, revocations, expiries |
| **Channel templates** | Templates created and removed; temporary channels created and deleted |
| **Private channels** | System configuration changes, rooms created and deleted, ownership claims |
| **Tickets** | Tickets opened, claimed, released, moved, closed |
| **Automod** | Anti-flood and anti-advertising violations |
| **Automod AI** | Anti-insult violations only |

**Automod AI** is deliberately its own category. AI verdicts are the ones a human should
review; mixing them into the same channel as mechanical flood detections buries them.

---

## A routing that works

Make a staff-only category with a handful of channels rather than one firehose:

| Channel | Categories |
|---|---|
| `#log-moderation` | Moderation |
| `#log-automod` | Automod, Automod AI |
| `#log-tickets` | Tickets |
| `#log-channels` | Channel templates, Private channels |
| `#log-general` | General, Commands |

The split that matters most is **Moderation** away from **Automod**: one is your team's
work, the other is the filter's. Reading them interleaved makes both harder.

---

## Colors

Give each category a color and you can identify an embed before reading it. Red for
Moderation, orange for Automod, blue for Tickets, grey for General.

Note that **Moderation** goes further: individual sanction types carry their own colors,
set in [Moderation](Configuration-Moderation#embed-colors) — red bans, green unbans,
orange warns. Those override the category color for their own events. The category color
here is the fallback for anything without its own.

---

## Requirements

The destination must be a **text channel** on the same server, and the bot needs
**View Channel**, **Send Messages** and **Embed Links** in it.

If the channel is deleted or the bot loses access, the log is dropped silently. The
action it was reporting still happened — you just do not hear about it. Worth
re-checking after any permission overhaul.

Some categories are gated by the server's plan. A category your plan does not include is
skipped even with a channel configured.

---

## Ticket transcripts are different

Transcripts do **not** follow this routing. They go to the **log channel configured on
each ticket panel**. See [Tickets](Configuration-Tickets#transcripts).

---

## Do this now

1. Create a staff-only channel — `#log-general` will do to start.
2. Open **General** and **Moderation** and point both at it.
3. Give them different colors.
4. Come back and split them out once you know what volume looks like.

---

Next: **[Moderation](Configuration-Moderation)**
