# Configuration — Bump ME

**English** · [Italiano](IT-Configurazione-Bump)

*Dashboard → your server → **Bump ME***

`/bump` writes your server into the **bot's own Discord description** — the text on the
bot profile, visible from every server it is in — and holds it there for 12 to 24 hours.

Requires the **Basic** plan. It is **off** by default.

---

## Understand this first

VionDefence is one Discord application with **one** description. It is not one slot per
server: while any server anywhere holds it, `/bump` everywhere else answers with the
time it frees up.

The window is drawn at random between 12 and 24 hours on every bump, so the slot never
reopens at a predictable hour that one server could sit and wait for.

---

## Set it up

1. Paste a **non-expiring invite** for your server.
2. Optionally set a **server name** — leave it empty to use the Discord server name.
3. Optionally set **XP for running `/bump`**.
4. Turn **Bump ME on** and save.

The link is checked for shape when you save (`discord.gg/…`, `discord.com/invite/…` or
`discordapp.com/invite/…`), and the feature cannot be turned on without one.

Create a **never-expiring** invite for this. The bot does not test the link, so a
24-hour invite pasted here will spend most of its window pointing nowhere.

| Setting | Meaning |
|---|---|
| **Turn Bump ME on** | While off, `/bump` says the feature is disabled here |
| **Server name** | The name in the description. Empty uses the Discord name |
| **Invite link** | Where the description sends people |
| **XP for running `/bump`** | Paid to whoever ran it. 0 pays nothing |

---

## What gets written

While your server holds the slot:

```
Bot bumped by ${server-name}: ${server-url}

VionDefence Security Protection Managing.
Support Discord: https://discord.gg/CUPvkc87CY
```

The rest of the time:

```
VionDefence Security Protection Managing.
Support Discord: https://discord.gg/CUPvkc87CY
```

The panel previews both with your own values filled in before you save.

---

## The XP reward

Only paid when the [level system](Configuration-Levels) is on. It goes up the same
ladder as any other XP, so a bump can push someone over a level and hand out that
level's rewards.

Keep it modest. Making `/bump` the fastest way to climb turns your leaderboard into a
race to run one command, which is not what the ladder is meant to measure.

---

## Who can run it

`/bump` is open to everyone by default. Restrict it from
[Commands](Configuration-Commands) — by permission, role or channel — like any other
command.

Consider limiting it to a role. Everyone racing for the slot means whoever is awake
gets it, and the reply to the rest is always "taken, come back later".

---

## Restarts and downgrades

**On a bot restart** the description returns to the default and the slot is released,
so `/bump` works again straight away. A bump does not survive a restart.

**If your plan drops below Basic**, or the bot is removed from the server, a bump you
were holding is released immediately and the description is restored.

---

## Checking on it

The panel shows whether the slot is free, taken by someone else, or held by you and
until when. Below it sit your last ten bumps: who ran each, when, and the XP it paid.

Bumps and expiries are also written to the **Levels**
[log category](Configuration-Logs).

---

## Common problems

**`/bump` says the feature is disabled.** It is off in the panel, or the plan dropped
below Basic.

**`/bump` says there is no invite link.** The link field is empty. Note the feature
cannot be turned on without one, so this normally means it was cleared afterwards.

**"Another server is being sponsored".** Working as intended — one slot for the whole
bot. The reply says when it frees up.

**The bump vanished.** The bot restarted. The slot is free again; run `/bump` once more.

---

Next: [Levels](Configuration-Levels) · [Commands](Configuration-Commands)
