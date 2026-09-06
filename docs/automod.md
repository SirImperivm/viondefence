# Automod

**English** · [Italiano](it/automod.md)

Automod watches messages and reacts to violations. It has three independent modules,
all **disabled by default**.

Configure it in the dashboard under **Automod**.

---

## Action modes

Every module has the same two-mode switch:

| Mode | What happens on a violation |
|---|---|
| **Passive** | The message is handled and the violation is logged. No sanction. |
| **Passive + active** | Same, plus an automatic sanction chosen by you. |

In **passive + active** you pick the **active action** — `warn`, `kick`, `ban`, `mute`
or `timeout` — and, for the ones that take one, a **duration**. You can also set a
custom **reason** that is recorded on the sanction and shown to the member.

Sanctions applied by automod go through the normal moderation pipeline: they land in
`/userhistory`, they respect the mute role, and temporary ones expire on schedule.
The bot itself is recorded as the issuing moderator.

> A `timeout` active action without a duration does nothing. Set one.

---

## Exemptions

Three settings apply to **all** modules at once:

| Setting | Effect |
|---|---|
| **Exempt roles** | Members with any of these roles are never checked |
| **Exempt users** | These specific members are never checked |
| **Respect role hierarchy** | When on, members ranked **above the bot** are never checked |

Leave *Respect role hierarchy* on unless you have a reason not to — it stops automod
from repeatedly attempting actions Discord will reject anyway.

Bot messages and system messages are always ignored.

---

## Anti-flood

Catches message spam and copy-paste repetition.

| Setting | Default | Meaning |
|---|---|---|
| **Max messages** | 5 | How many messages inside the window trip the filter |
| **Interval** | 7 s | The sliding window the messages are counted in |
| **Max duplicate messages** | 3 | How many identical messages in a row trip the filter |

Both conditions are checked independently: 5 different messages in 7 seconds is
flooding, and so is the same message posted 3 times.

Counting is **per member, per server** and resets when the window slides past.

---

## Anti-advertising

Catches invites and links.

| Setting | Default | Meaning |
|---|---|---|
| **Block Discord invites** | on | Blocks `discord.gg/…` and `discord.com/invite/…` links |
| **Block links** | on | Blocks any `http://` or `https://` URL |
| **Whitelisted domains** | empty | Domains that are always allowed |

The two blocks are separate. Turn off *Block links* and keep *Block Discord invites*
on if you want to allow the open web but not server advertising.

**Whitelisted domains** only affects *Block links*: add `youtube.com`, `github.com`
and so on to let them through while everything else is caught.

---

## Anti-insult

The only AI-backed module. It reads the message, judges whether it is an insult, and
rates how severe it is.

| Setting | Default | Meaning |
|---|---|---|
| **Sensitivity** | medium | How strict the filter is |
| **Context messages** | 5 | How many preceding messages are sent along for context |

### Sensitivity

| Sensitivity | Catches |
|---|---|
| **Low** | Only severe insults |
| **Medium** | Moderate and severe insults |
| **High** | Everything, including mild ones |

Higher sensitivity means more false positives. Start at **medium**, run the module in
**passive** for a few days, read the log, and only then decide whether to turn on an
active action.

### Context

**Context messages** gives the classifier the preceding messages in the channel so it
can tell a joke between friends from an actual attack. More context is more accurate
and slightly slower. `5` is a reasonable default; `0` judges each message in isolation.

Anti-insult violations are logged to their own category — **Automod AI** — separate
from the other two modules, so you can route them to a different channel and review
them without noise.

---

## Recommended rollout

1. Enable a module in **passive** mode.
2. Point the **Automod** (and **Automod AI**) log categories at a staff-only channel —
   see [Logs](logs.md).
3. Watch for a few days. Add exempt roles for staff and bots you trust.
4. Adjust thresholds and whitelists until the log is mostly true positives.
5. Only then switch to **passive + active**, starting with a mild action like `warn`.

Going straight to `ban` on an untuned filter is how you lose members to a false
positive.

---

Next: [Voice channels](voice-channels.md)
