# Bump ME

**English** · [Italiano](it/bump.md)

`/bump` puts your server in the **bot's own Discord description** — the text everyone
reads on the bot profile, in every server it is in. It stays there for a window drawn
at random between 12 and 24 hours, then the description goes back to normal and the
next server can take it.

Available from the **Basic** plan.

---

## One slot for everyone

VionDefence is one Discord application with one description, so **one server at a
time** can be sponsored. This is not a per-server cooldown: while any server holds the
slot, `/bump` on every other server answers with when it frees up.

The window is drawn fresh on each bump, somewhere between 12 and 24 hours, so the slot
does not reopen at a predictable hour that a single server could camp.

---

## What the description says

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

The dashboard shows both, filled in with your own name and link, before you save.

---

## Configuration

The **Bump ME** panel has its own entry in the dashboard sidebar, under *Promotion*.

| Setting | What it does |
|---|---|
| **Turn Bump ME on** | While off, `/bump` answers that the feature is disabled here |
| **Server name** | The name written into the description. Empty uses the Discord server name |
| **Invite link** | Your invite, e.g. `https://discord.gg/yourcode` |
| **XP for running `/bump`** | XP handed to whoever ran it. Zero gives nothing |

The invite link must be a real Discord invite (`discord.gg/…`, `discord.com/invite/…`
or `discordapp.com/invite/…`); anything else is refused when you save. You cannot turn
the feature on without setting a link first — `/bump` would only be able to answer
with an error.

Use a **non-expiring** invite. The bot does not check whether the link still works, so
an expired one would sit in the description doing nothing for the whole window.

### The XP reward

The XP only lands if the [level system](levels.md) is on. It goes through the same
ladder as any other XP: it can push the member up a level, which hands out that
level's rewards and posts the usual notice.

---

## Running it

`/bump` is available to everyone by default; restrict it from the **Commands** section
like any other command if you would rather only staff ran it.

| Answer | Meaning |
|---|---|
| Server bumped | The description now carries your server, until the time shown |
| Another server is being sponsored | The slot is taken; it frees up at the time shown |
| Bump ME is turned off | Turn it on in the dashboard |
| No invite link set | Add one in the dashboard |

The confirmation shows the name, the link and when the slot frees up, plus the XP
earned when there is any.

---

## When the bot restarts

On boot the description goes back to the default one and the slot is released, so
`/bump` is immediately available again. A bump does not survive a restart of the bot.

This is deliberate: the bot cannot keep promising a sponsorship it stopped displaying
while it was down, and leaving the slot locked would block every server for hours over
a restart nobody asked for.

---

## When a plan ends

A server that drops below Basic loses the feature. If it was holding the slot at the
time, the description is restored and the slot frees up immediately.

The same happens if the bot is removed from a server that was holding the slot.

---

## Logs

Bumps and their expiry are recorded in the **Levels** log category — see
[Logs](logs.md). The dashboard also keeps the last ten bumps of your server, with who
ran each one, when, and how much XP it paid.

---

Next: [Logs](logs.md)
