# Configuration — Moderation

**English** · [Italiano](IT-Configurazione-Moderazione)

*Dashboard → your server → **Moderazione***

Five sanction cards — kick, ban, warn, mute, timeout — plus the warn escalation panel.

---

## The mute role

Set it on the **mute** card. Until you do, every `/mute` and every automod `mute` action
fails.

A mute role that actually works:

1. Create a role in Discord — call it `Muted`. Give it no permissions of its own.
2. In your channel permissions, **deny** it *Send Messages*, *Speak*, *Add Reactions*
   and *Send Messages in Threads*.
3. In **Server Settings → Roles**, put **VionDefence above the mute role**. A bot
   cannot assign a role that sits above its own.
4. Select the role in the dashboard.

Step 3 is the one that gets missed. Everything looks configured and mutes still fail.

---

## DM notifications

Each of the five cards has its own **Notify the user by DM** toggle. When on, the
sanctioned member gets a direct message with the type, the reason and the duration.

All five default to **on**.

The DM is best-effort. If the member has DMs from server members closed, or has already
left, the sanction still applies and nothing is treated as an error.

Turning these off for `warn` is a common choice on servers where warns are used as
internal notes rather than as a message to the member.

---

## Embed colors

Each sanction card carries two colors, used on the **Moderation** log embeds for that
sanction type:

| Field | Used when |
|---|---|
| **Embed color (applied)** | The sanction is issued — a ban, a warn, a mute |
| **Embed color (lifted)** | The sanction is revoked by a moderator, or expires on its own |

The second field only appears on sanctions that can be lifted — **ban**, **warn**,
**mute** and **timeout**. A kick has nothing to revoke, so it has a single color.

This is what lets a log channel be read at a glance: red for a ban going out, green for
the unban coming back, orange for a warn.

### Defaults

| Sanction | Applied | Lifted |
|---|---|---|
| **Kick** | `#F76B15` orange | — |
| **Ban** | `#E5484D` red | `#46A758` green |
| **Warn** | `#F5A623` amber | `#46A758` green |
| **Mute** | `#8E4EC6` purple | `#46A758` green |
| **Timeout** | `#3E63DD` blue | `#46A758` green |

Change any of them with the color picker, or by typing a `#RRGGBB` value.

These colors take priority over the **Moderation** category color set in
[Logs](Configuration-Logs) — that one remains the fallback for any moderation event
without a color of its own.

---

## Warn expiry

How long a warn stays **active**.

- **Empty** — warns never expire on their own. They stay active until a moderator
  removes them with `/warn remove` or `/warn clear`.
- **Set** — a warn deactivates automatically once it reaches that age.

Expired warns are not deleted. They stay in `/userhistory` with the status **expired**,
so the record survives even after the warn stops counting.

Only **active** warns count toward escalation.

---

## Warn escalation

Turns a count of active warns into an automatic sanction.

Each rule has:

| Field | Meaning |
|---|---|
| **Threshold** | A number of active warns |
| **Action** | `kick`, `ban`, `mute` or `timeout` |
| **Duration** | For the actions that take one |
| **Reason** | Optional. Left empty, a default mentioning the warn count is used |

### A worked example

| Threshold | Action | Duration |
|---|---|---|
| 3 | mute | 1h |
| 5 | timeout | 1d |
| 7 | ban | 7d |

Third active warn → one-hour mute. Fifth → one-day timeout. Seventh → one-week ban.

### The rule that surprises people

Rules match the active warn count **exactly**, at the moment a warn is added. A
threshold-3 rule fires on the third active warn and does not fire again on the fourth.

The consequence: a member sitting at 4 warns who has one removed and then earns a new one
passes through 3 again — and re-triggers the threshold-3 rule. Clearing warns is how you
give someone a clean slate; just know what it replays.

Several rules can share a threshold. All of them fire.

A `timeout` rule with no duration is skipped — Discord timeouts always need one.

---

## Checking what is in force

The colors and DM settings on this page describe what happens when a sanction is
issued. To read the state back, four commands work off the same configuration:

- `/userinfo user:@member` — the member's whole moderation status in one embed:
  banned, muted or timed out, active warn count, every active sanction with its ID,
  totals per type. Its color is the one you set here for the most severe sanction
  still active on them.
- `/ban list`, `/mute list`, `/timeout list`, `/warnings` — everything of that kind
  active on the server right now, paginated.
- `/ban info`, `/mute info`, `/timeout info`, `/warn info` — one sanction in full,
  looked up by its ID.

All four are configured like any other command, in the **Commands** section: enable
them, and decide which roles, permission and channels may use them.

`/userinfo` is also the fastest way to catch a drift between Discord and the sanction
database — a manual Discord ban with no sanction behind it, a mute role left on a
member, or a timeout sanction Discord already dropped.

---

## Automatic expiry

Every 30 seconds the bot lifts what is due: temporary bans are unbanned, mutes lose the
role, warns are marked expired. The member gets a DM, and the event is written to the
**Moderation** log with the sanction's *lifted* color.

If the bot is offline when something comes due, it lifts on the first sweep after it
restarts.

---

## Do this now

1. Create the mute role, deny it the right permissions, and put VionDefence above it.
2. Select it on the **mute** card.
3. Glance at the embed colors — the defaults are sensible, change them if your log
   channel has a theme.
4. Leave warn expiry and escalation empty until you know how your team actually uses
   warns.

---

Next: **[Commands](Configuration-Commands)**
