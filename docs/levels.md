# Level system

**English** · [Italiano](it/livelli.md)

Members earn XP by writing in chat and by spending time in voice channels. XP buys
levels, levels hand out rewards. Everything is automatic once configured: there is no
command to give or take XP by hand.

Available from the **Free** plan.

---

## How XP is earned

There are three sources, and each can be turned off on its own by setting its value
to zero.

| Source | How much | When it is written |
|---|---|---|
| Text messages | `XP per message`, once per cooldown window | Immediately |
| Voice time | `XP per minute` × whole minutes connected | When the member leaves voice |
| `/bump` | The XP set in the [Bump ME](bump.md) panel | Immediately |

### Text

Every message sent in a counted channel earns the configured XP, but only once per
**cooldown** (60 seconds by default). Without a cooldown a member could flood a
channel and climb in seconds; with one, the level ladder measures presence rather
than typing speed.

Messages deleted by the automod or the content filter still earn XP: the two systems
run independently.

### Voice

Voice time is measured from when a member joins a counted channel to when they leave
it. Only **whole minutes** count — 90 seconds is one minute's worth of XP.

Moving from one voice channel to another **on the same server** does not end the
session: the XP of each leg is added up and written together. This is why the
level-up notice only fires when the member leaves voice altogether, and why a member
hopping between five channels gets one notice rather than five.

If the bot restarts while a member is connected, the time earned so far is written
before it goes down, and the timing starts again from the boot.

---

## Where XP is earned

The **Where XP is earned** panel holds three lists — categories, text channels and
voice channels — plus a list of roles that never earn anything.

The rule is:

- **All three lists empty** → every channel of the server counts.
- **Any entry added** → only the listed channels, and every channel inside the listed
  categories, count.

A category covers whatever is inside it at the time, so a channel moved into a
counted category starts counting without any change here.

Bots never earn XP, whatever the lists say.

---

## The level curve

Three settings decide how expensive the ladder is.

| Setting | What it does |
|---|---|
| **Minimum XP per level** | The base cost. A level never costs less than this. |
| **XP multiplier** | A formula: the base cost is multiplied by whatever it produces. |
| **Last level** | The top of the ladder. XP earned past it is not stored. |

The cost of level *N* is `minimum XP × multiplier(N)`, rounded, and never below the
minimum. The dashboard shows the first ten levels as you type, so the shape of the
curve is visible before it is saved.

### Writing the multiplier

The multiplier is an arithmetic expression. It may use:

| Placeholder | Value |
|---|---|
| `{level}` | The level being priced, starting at 1 |
| `{base_xp}` | The minimum XP per level |
| `{max_level}` | The last level |
| `{previous}` | What the level before this one cost |

Operators `+ - * / % ^`, brackets, and the functions `min`, `max`, `pow`, `floor`,
`ceil`, `round`, `abs`, `sqrt` and `log`. Nothing else is accepted — a formula that
uses anything outside this list is refused when you save it, with the reason.

### Examples

| Formula | Shape | Level 1 / 5 / 10 cost, base 100 |
|---|---|---|
| `1` | Flat — every level costs the same | 100 / 100 / 100 |
| `1 + ({level} - 1) * 0.5` | Gentle, the default | 100 / 300 / 550 |
| `{level}` | Linear | 100 / 500 / 1000 |
| `{level} ^ 1.5` | Steep | 100 / 1118 / 3162 |
| `min({level}, 20)` | Rises then flattens at level 20 | 100 / 500 / 1000 |

A formula whose cost overflows what can be counted, or lands at zero or below, is
refused rather than saved: it would leave members stuck at a level they can never
pass.

### Changing the curve later

The curve is worked out from the XP each member already holds, so changing it moves
everybody at once — nobody loses XP, but a member sitting at level 12 on a cheap
curve may find themselves at level 7 on an expensive one. Rewards already handed out
are not taken back.

Lowering the **last level** drops the rewards pinned above the new top, since they
could never fire again.

---

## Rewards

Each level can carry up to two rewards: a **role** and a **written reward**.

- **Role** — given the moment the level is reached, and never taken away. The bot
  needs *Manage Roles* and must sit **above** that role in the role list; the
  dashboard refuses a role it could not hand out.
- **Written reward** — a line of text added to the level-up notice.

A member who crosses several levels in one go — a long voice session, for instance —
receives the rewards of **every** level crossed, but only one notice.

How many rewards you can set depends on the plan: 10 on Free, 25 on Basic, 50 on Pro,
100 on Ultimate. Lowering the plan trims the list from the highest levels down.

### Placeholders

Both the level-up notice and the written rewards accept:

| Placeholder | Replaced with |
|---|---|
| `{user}` | A mention of the member |
| `{username}` | Their Discord username |
| `{displayname}` | Their nickname on this server |
| `{level}` | The level just reached |
| `{previous_level}` | The level they were at |
| `{xp}` | Their total XP |
| `{guild}` | The server name |

---

## The level-up notice

Set a text channel for it, or leave the channel empty to send it in **direct
messages** instead. If the chosen channel is deleted or is not a text channel, the
notice falls back to a DM rather than being lost.

A member with DMs closed simply does not receive the fallback; the level and the
rewards are still applied.

Separately from the notice, the **Levels** log category records every level-up for
the staff — see [Logs](logs.md).

---

## Commands

`/level [user]` shows the level, the total XP, the rank on the server and the XP
missing for the next level. Without the `user` option it answers for whoever ran it.

`/userinfo` carries the same figures in a **Level** field, alongside the moderation
picture — but only on servers where the level system is on.

See [Commands](commands.md) for the full reference.

---

## Leaderboard

The dashboard lists every member who has earned XP, ordered by total XP, with their
level, their message count and their minutes in voice. It is read-only: the ladder is
built entirely from what members actually did.

---

Next: [Bump ME](bump.md)
