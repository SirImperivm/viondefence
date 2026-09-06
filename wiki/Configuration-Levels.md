# Configuration — Levels

**English** · [Italiano](IT-Configurazione-Livelli)

*Dashboard → your server → **Levels***

Members earn XP for taking part, XP buys levels, levels hand out rewards. It runs on
its own once set up — there is no command to hand out XP by hand.

Included from the **Free** plan. It is **off** by default.

---

## Set it up in five minutes

1. Turn **the level system on**.
2. Leave the curve at its defaults (base 100, multiplier `1 + ({level} - 1) * 0.5`,
   last level 100). It is a sane ladder — you can tune it later without losing anything.
3. Leave the whitelists **empty** for now: every channel counts.
4. Pick an **announcement channel** — somewhere members actually read.
5. Save, and send a message to check the XP starts moving.

Add rewards afterwards, once you can see how fast people are actually climbing.

---

## How XP is earned

| Setting | Default | Meaning |
|---|---|---|
| **XP per message** | 5 | Earned by a message in a counted channel |
| **Cooldown** | 60 s | A member earns from a message at most once per window |
| **XP per minute in voice** | 2 | Earned per whole minute in a counted voice channel |

Set a value to **0** to switch that source off without turning the whole system off.

Do not set the cooldown to 0. With no cooldown the ladder measures typing speed rather
than participation, and the fastest way up becomes flooding a quiet channel.

### The voice session

Voice time runs from joining to leaving, counted in whole minutes. Moving between
voice channels of the same server **continues the same session**: the legs are added up
and written together, so the level-up notice fires once, when the member finally leaves
voice — not on every hop.

---

## Where XP is earned

Three lists — categories, text channels, voice channels — plus roles that never earn.

| Whitelists | What counts |
|---|---|
| All empty | Every channel of the server |
| Any entry added | Only the listed channels, and everything inside the listed categories |

Listing a **category** covers whatever is inside it at the time, so channels moved in
later start counting on their own. This is usually what you want: list the categories,
not the individual channels.

Exclude AFK channels, bot-command channels and music channels. XP for sitting in an AFK
channel overnight makes the whole ladder meaningless.

---

## The level curve

| Setting | Default | Meaning |
|---|---|---|
| **Minimum XP per level** | 100 | The base cost. A level never costs less |
| **XP multiplier** | `1 + ({level} - 1) * 0.5` | A formula the base is multiplied by |
| **Last level** | 100 | The top of the ladder |

The cost of a level is `minimum XP × multiplier`, rounded. The panel prints the first
ten levels as you type: watch that table rather than trusting the formula.

### The formula

Placeholders: `{level}`, `{base_xp}`, `{max_level}` and `{previous}` (what the level
before cost). Operators `+ - * / % ^`, brackets, and `min`, `max`, `pow`, `floor`,
`ceil`, `round`, `abs`, `sqrt`, `log`. Anything else is refused when you save, with the
reason — it is a maths expression, not code.

| Want | Write |
|---|---|
| Every level costs the same | `1` |
| A gentle climb | `1 + ({level} - 1) * 0.5` |
| Each level costs its own number of bases | `{level}` |
| A steep climb | `{level} ^ 1.5` |
| Steep at first, flat after level 20 | `min({level}, 20)` |

### Changing it later

Levels are worked out from the XP each member already holds, so a new curve moves
everybody at once. Nobody loses XP, but an expensive curve can drop a member from level
12 to level 7. Rewards already given are not taken back.

Decide the curve before you announce the system. Members notice a level going backwards
far more than they notice one arriving late.

---

## Rewards

Each level takes up to two: a **role** and a **written reward**.

- **Role** — given on reaching the level, never removed. The bot needs *Manage Roles*
  and must sit **above** the role; the dashboard refuses roles it could not hand out,
  so a rejection here means the bot is too low in the role list.
- **Written reward** — a line added to the level-up notice.

Crossing several levels at once — after a long voice session — hands out **every**
crossed level's rewards, with a single notice.

Plan limits: 10 rewards on Free, 25 on Basic, 50 on Pro, 100 on Ultimate.

Placeholders for the notice and the written rewards: `{user}`, `{username}`,
`{displayname}`, `{level}`, `{previous_level}`, `{xp}`, `{guild}`.

---

## The notice

Choose a text channel, or leave it empty to send the notice in **direct messages**.
If the chosen channel disappears, the notice falls back to a DM instead of being lost.

Separately, the **Levels** [log category](Configuration-Logs) records every level-up for
staff, including reward roles that could not be handed out. Point it at a staff channel
— it is where you will find out the bot is sitting below a reward role.

---

## What members see

`/level [user]` shows the level, the XP, the rank and the progress to the next level.
`/userinfo` carries the same figures in a **Level** field.

The dashboard shows the full **leaderboard**, with messages and voice minutes per
member.

---

## Common problems

**Nobody is earning XP.** The system is off, or every relevant channel sits outside the
whitelists. Remember an empty whitelist counts everything — a half-filled one does not.

**The reward role is not being given.** The bot is below that role in the role list, or
has lost *Manage Roles*. Check the **Levels** log category: the failure is written there
with the role named.

**Levels dropped after I changed the curve.** Expected: levels are recomputed from
existing XP. Put the old numbers back and they return.

**Voice XP is not arriving.** It is written when the member **leaves** voice, not while
they sit there. Check after they disconnect.

---

Next: [Bump ME](Configuration-Bump) · [Logs](Configuration-Logs)
