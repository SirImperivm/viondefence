# Member counters

**English** · [Italiano](it/contatori.md)

Voice channels that show how many people are on the server, kept up to date on their
own. Everyone can see them, nobody can join them: they are signs, not rooms.

Available from the **Free** plan.

---

## What gets created

Turning the feature on creates three voice channels:

| Channel | Counts | Placeholder |
|---|---|---|
| Everyone | Every member, bots included | `{total-count}` |
| Bots | Only bots | `{bots-count}` |
| Members | Everyone except bots | `{members-count}` |

A **fourth** channel is optional and counts your staff, based on a list of roles you
choose: `{staff-count}`. A member holding any one of those roles is counted once.

Each channel is created with `View Channel` allowed and `Connect` denied for
`@everyone`, so they are visible in the list but cannot be entered.

Turning the feature off deletes the channels. Nothing is lost: the numbers are read
from Discord every time, never stored.

---

## Names

The name is yours; only the placeholder is replaced.

```
👥 All: {total-count}      →      👥 All: 1247
🛡 Staff: {staff-count}     →      🛡 Staff: 9
```

A name must contain its own placeholder — the dashboard refuses it otherwise, since a
counter that never changes is just a channel with a confusing name. Names are capped
at Discord's 100 characters.

---

## How often it refreshes

**Discord allows two channel renames every ten minutes.** Past that the request is not
rejected, it is queued — so a counter set to refresh every minute would silently fall
behind exactly while appearing to be the most up to date.

Because of that the refresh interval has a floor of **five minutes**, and defaults to
ten. The bot also skips a rename when the new name is identical to the current one, so
a quiet server does not burn its allowance on nothing.

---

## `/server stats`

Sends the same numbers as an ephemeral message, visible only to whoever ran it, and
**recalculates on the spot** — it does not read the channel names.

It also reports how many of those members and staff are **online**, which the channels
cannot show.

| Option | Required | Description |
|---|---|---|
| *(none)* | | `/server stats` takes no options |

The command works whether or not the counter channels are on: with them on it also
takes the chance to realign the channels.

Online figures need Discord's **Presence** intent. Without it the command says so in
the footer and shows only the totals, rather than reporting zero — which would be a
wrong number rather than a low one.

---

## Permissions

VionDefence needs **Manage Channels** to create, rename and delete the counters. If it
loses that permission the channels stay as they are, with the last numbers written.

Put the channels in a category if you want them grouped, or leave the category empty to
have them at the top of the server.

---

Next: [Level system](levels.md)
