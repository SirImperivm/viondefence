# Configuration — Automod

**English** · [Italiano](IT-Configurazione-Automod)

*Dashboard → your server → **Automod***

Three independent filters, all **off** by default. Read the rollout section before you
turn any of them on with an action attached.

---

## Action modes

Every module has the same switch:

| Mode | On a violation |
|---|---|
| **Passive** | The message is handled and the violation is logged. No sanction. |
| **Passive + active** | The same, plus a sanction you choose. |

In **passive + active** you pick the action — `warn`, `kick`, `ban`, `mute` or
`timeout` — a **duration** where one applies, and an optional **reason** recorded on the
sanction and shown to the member.

Automod sanctions go through the normal moderation pipeline: they appear in
`/userhistory`, respect the mute role, use the sanction's
[embed colors](Configuration-Moderation#embed-colors), and expire on schedule. The bot
is recorded as the issuing moderator.

A `timeout` action with **no duration does nothing**. Set one.

---

## Exemptions

Three settings that apply to all three modules at once:

| Setting | Effect |
|---|---|
| **Exempt roles** | Members holding any of these are never checked |
| **Exempt users** | These specific members are never checked |
| **Respect role hierarchy** | When on, members ranked above the bot are never checked |

Leave *Respect role hierarchy* on unless you have a specific reason. It stops the bot
repeatedly attempting actions Discord will refuse anyway.

Bot messages and system messages are always ignored.

Add your staff roles to **exempt roles** early. Moderators posting links in a staff
channel is the single most common false positive.

---

## Anti-flood

Message spam and copy-paste repetition.

| Setting | Default | Meaning |
|---|---|---|
| **Max messages** | 5 | How many messages in the window trip it |
| **Interval** | 7 s | The sliding window |
| **Max duplicate messages** | 3 | How many identical messages in a row trip it |

The two conditions are checked separately: 5 different messages in 7 seconds is flooding,
and so is the same message three times. Counting is per member per server, and resets as
the window slides.

If you run a busy general chat, raise **max messages** before you raise the interval —
excitable conversation looks like flooding at 5/7s.

---

## Anti-advertising

| Setting | Default | Meaning |
|---|---|---|
| **Block Discord invites** | on | Blocks `discord.gg/…` and `discord.com/invite/…` |
| **Block links** | on | Blocks any `http://` or `https://` URL |
| **Whitelisted domains** | empty | Always allowed |

The two blocks are independent. The common configuration is **block invites on, block
links off** — you do not want other servers advertised, but you do want people sharing a
YouTube video.

If you keep **block links** on, put `youtube.com`, `github.com`, `tenor.com` and
whatever else your community uses into the whitelist. The whitelist only affects *block
links*, not the invite blocker.

---

## Anti-insult

The AI-backed module. It reads the message, decides whether it is an insult, and rates
the severity.

| Setting | Default | Meaning |
|---|---|---|
| **Sensitivity** | medium | How strict |
| **Context messages** | 5 | How many preceding messages go along for context |

| Sensitivity | Catches |
|---|---|
| **Low** | Severe insults only |
| **Medium** | Moderate and severe |
| **High** | Everything, including mild |

**Context messages** is what lets the classifier tell a joke between friends from a real
attack. More context is more accurate and slightly slower. `5` is a good default; `0`
judges each message alone and will misread banter.

Violations go to the **Automod AI** log category, separate from the other two modules —
route it somewhere your staff will actually read. See [Logs](Configuration-Logs).

---

## How to roll this out

Turning on `ban` on an untuned filter is how you lose members to a false positive. Do
this instead:

1. Enable one module in **passive**.
2. Point **Automod** and **Automod AI** at a staff-only channel.
3. Watch for a few days. Add exempt roles for staff and for bots you trust.
4. Tune thresholds and whitelists until the log is mostly true positives.
5. Only then switch to **passive + active**, and start with `warn`.
6. Escalate the action later, once the log has earned your trust.

One module at a time. Three untuned filters firing at once is impossible to attribute.

---

Next: **[Logs](Configuration-Logs)** · back to **[Home](Home)**
