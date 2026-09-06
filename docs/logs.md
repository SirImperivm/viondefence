# Logs

**English** · [Italiano](it/log.md)

VionDefence writes an embed to Discord for everything it does. Logging is split into
**nine independent categories**, each routed to its own channel and styled on its own.

Configure them in the dashboard under **Logs**.

---

## Categories

| Category | What lands here |
|---|---|
| **General** | Server-level events and bot errors that do not belong elsewhere |
| **Commands** | Command usage |
| **Moderation** | Kicks, bans, mutes, timeouts, warns, revocations, expiries |
| **Channel templates** | Templates created, removed, cleared; temporary channels created and deleted |
| **Private channels** | System configuration changes, rooms created and deleted, ownership claims |
| **Tickets** | Tickets opened, claimed, released, moved, closed |
| **Automod** | Anti-flood and anti-advertising violations |
| **Automod AI** | Anti-insult violations only |
| **Content filter** | Messages removed because their content is not allowed in that channel |

**Automod AI** is deliberately separate from **Automod**: AI verdicts are the ones you
want to review by hand, and mixing them with mechanical flood detections buries them.

---

## Per-category settings

| Setting | Meaning |
|---|---|
| **Channel** | Where embeds for this category are sent |
| **Color** | The embed's left border color, as a hex value |
| **Thumbnail URL** | An image shown in the embed's corner. Optional |

Leaving the **channel** empty disables that category — nothing is sent, and nothing
fails. That is the intended way to turn a category off.

The default color is `#777777` and no thumbnail.

The **Moderation** category is a special case: individual sanction types carry their
own colors, and those take priority over the category color for their own events.
See [Moderation](moderation.md#log-embed-colors).

Colors are worth setting: at a glance, red for Moderation and orange for Automod tells
you what happened before you read a word.

---

## Requirements

The destination must be a **text channel** in the same server, and VionDefence needs
**View Channel**, **Send Messages** and **Embed Links** in it.

If the channel is deleted or the bot loses access, the log is dropped silently — the
action it was reporting still happened.

Some log categories may not be available on every plan. A category your plan does not
include is skipped even if a channel is configured for it.

---

## A practical setup

A staff-only category with:

| Channel | Categories routed to it |
|---|---|
| `#log-moderation` | Moderation |
| `#log-automod` | Automod, Automod AI |
| `#log-tickets` | Tickets |
| `#log-channels` | Channel templates, Private channels |
| `#log-general` | General, Commands |

Splitting Moderation from Automod matters most: one is your team's work, the other is
the filter's. Reviewing them together makes both harder to read.

Ticket **transcripts** do not follow this routing — they go to the **log channel set on
each ticket panel**. See [Tickets](tickets.md#closing-and-transcripts).

---

## Timestamps

Every embed is timestamped. The timezone and format come from the server's **General**
settings — see [Getting started](getting-started.md#3-set-the-basics).

---

Next: [FAQ](faq.md)
