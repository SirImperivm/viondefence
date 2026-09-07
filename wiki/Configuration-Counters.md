# Configuration — Counters

**English** · [Italiano](IT-Configurazione-Contatori)

*Dashboard → your server → **Counters***

Voice channels that show how many people are on the server. Everyone sees them, nobody
joins them — they are signs, not rooms.

Included from the **Free** plan. They are **off** by default.

---

## Set it up in two minutes

1. Turn **the counters on**.
2. Leave the interval at ten minutes and the names as they are.
3. Save. The three channels appear straight away, already filled in.

Everything else — the category, the names, the staff counter — can wait until you have
seen them in place.

---

## The three channels

| Channel | Counts | Placeholder |
|---|---|---|
| Everyone | Every member, bots included | `{total-count}` |
| Bots | Only bots | `{bots-count}` |
| Members | Everyone except bots | `{members-count}` |

They are created with `View Channel` allowed and `Connect` denied for `@everyone`.
Don't add your own `Connect` allow on top: the channel would become enterable and stop
reading as a label.

Turning the counters off deletes the channels. Nothing is lost — the numbers come from
Discord each time and are never stored, so switching back on rebuilds them with the
current figures.

---

## The staff counter

A fourth, optional channel counting the members who hold **any one** of the roles you
pick. Somebody with three staff roles is still counted once.

The dashboard will not let you turn it on with an empty role list: the counter would
sit at zero forever and look broken.

Pick the roles that mean "staff" to your members, not every role your staff happens to
hold. A `@Verified` role in that list turns the staff counter into a second member
counter.

---

## Names

Write the name you want; only the placeholder is replaced.

```
👥 All: {total-count}      →      👥 All: 1247
🛡 Staff: {staff-count}     →      🛡 Staff: 9
```

Each name must contain its own placeholder — a name without one is refused, because a
counter that never changes is just a channel with a confusing title. Discord caps
channel names at 100 characters, and longer names are cut there.

---

## The refresh interval

**Discord allows two renames per channel every ten minutes.** Going past that does not
produce an error: the request is queued, and the counters quietly fall behind exactly
while looking like they update most often.

So the interval has a floor of **five minutes** and defaults to ten. The bot also skips
a rename whenever the new name matches the current one, so a quiet server keeps its
allowance for when the number actually moves.

If you want counts that react instantly, use `/server stats` — it recalculates on
demand, without touching the channels.

---

## `/server stats`

An ephemeral reply, visible only to whoever ran it, with the same numbers **plus how
many of those members and staff are online**.

It recalculates rather than reading the channel names, so it is also the quickest way
to check whether the counters are telling the truth.

Online figures need the **Presence** intent on the bot. Without it the reply says so
and shows only the totals, instead of reporting zero.

---

## Common problems

**The channels were not created.** The bot is missing **Manage Channels**, or the
category you picked no longer exists.

**A channel is stuck on an old number.** Either the rename allowance is spent — wait
out the ten-minute window — or the bot lost Manage Channels after creating it.

**Somebody deleted one of the channels.** The next refresh recreates it. You do not
need to turn the feature off and on.

**The staff counter says 0.** No role is selected, or the selected roles are not the
ones your staff actually hold.

**`/server stats` shows no online counts.** The Presence intent is off in the Discord
Developer Portal.

---

Next: [Levels](Configuration-Levels) · [Logs](Configuration-Logs)
