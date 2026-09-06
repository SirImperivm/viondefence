# Moderation

**English** · [Italiano](it/moderazione.md)

VionDefence records every sanction it applies, keeps it queryable, and expires
temporary sanctions on its own.

Configure it in the dashboard under **Moderation**.

---

## Sanction types

| Type | Backed by | Revocable | Supports a duration |
|---|---|---|---|
| **Kick** | Discord kick | no | no |
| **Ban** | Discord ban | yes | yes — or permanent |
| **Mute** | The server's mute role | yes | yes — or indefinite |
| **Timeout** | Native Discord timeout | yes | yes — **required**, max 28 days |
| **Warn** | VionDefence only | yes | expires after the warn expiry, if set |

A kick is a one-off event: there is nothing to revoke, so it stays in the history as
a closed record.

---

## The mute role

`/mute` and the automod `mute` action need a role to apply. Set it under
**Moderation → Mute role**.

Checklist for a mute role that actually works:

1. Create a role in Discord (e.g. `Muted`) with no permissions of its own.
2. In your channel permissions, deny it **Send Messages**, **Speak**, **Add
   Reactions** and **Send Messages in Threads**.
3. Position the **VionDefence** role **above** the mute role in Server Settings →
   Roles. A bot cannot assign a role that sits above its own.
4. Select the role in the dashboard.

Without step 3, mutes fail even though everything looks configured.

---

## DM notifications

Each sanction type has its own **DM notification** toggle. When it is on, the
sanctioned member receives a direct message with the type, the reason and the
duration.

All five are **on by default**.

The DM is best-effort: if the member has DMs from server members disabled, or has
already left the server, the sanction still applies and the failure is not treated as
an error.

---

## Log embed colors

Each sanction type carries its own colors, used on the **Moderation** log embeds:

| Field | Used when |
|---|---|
| **Embed color (applied)** | The sanction is issued |
| **Embed color (lifted)** | It is revoked by a moderator, or expires on its own |

The *lifted* color only exists for sanctions that can be lifted — **ban**, **warn**,
**mute** and **timeout**. A kick has nothing to revoke, so it has one color.

| Sanction | Applied | Lifted |
|---|---|---|
| Kick | `#F76B15` orange | — |
| Ban | `#E5484D` red | `#46A758` green |
| Warn | `#F5A623` amber | `#46A758` green |
| Mute | `#8E4EC6` purple | `#46A758` green |
| Timeout | `#3E63DD` blue | `#46A758` green |

These take priority over the **Moderation** category color set under
[Logs](logs.md#per-category-settings), which stays the fallback for any moderation event
without a color of its own.

---

## Warn expiry

**Warn expiry** decides how long a warn stays *active*.

- Leave it empty and warns never expire on their own — they stay active until a
  moderator removes them with `/warn remove` or `/warn clear`.
- Set a duration and each warn deactivates automatically once it is that old.

Expired warns are not deleted. They remain visible in `/userhistory` with the status
**expired**, so the paper trail survives even after the warn stops counting.

Only **active** warns count toward escalation.

---

## Warn escalation

Escalation turns a count of active warns into an automatic sanction.

A rule has a **threshold** (a number of active warns), an **action** (`kick`, `ban`,
`mute` or `timeout`), a **duration** for the actions that take one, and an optional
**reason** used on the automatic sanction. Leave the reason empty and a default one
mentioning the warn count is used instead.

A `timeout` rule with no duration is skipped — Discord timeouts always need one.

Rules fire on an **exact** match of the active warn count, at the moment the warn is
added. A rule with threshold `3` fires when the member's third active warn lands — it
does not fire again at the fourth.

### Example

| Threshold | Action | Duration |
|---|---|---|
| 3 | mute | 1h |
| 5 | timeout | 1d |
| 7 | ban | 7d |

A member reaching 3 active warns gets a one-hour mute. At 5, a one-day timeout.
At 7, a one-week ban.

You can attach more than one rule to the same threshold — all of them fire.

> Because rules match the count exactly, a member who is at 4 warns, gets one removed,
> then earns a new one will pass through 3 again and re-trigger the threshold-3 rule.
> Removing warns is the way to give someone a clean slate; be aware of what that
> replays.

---

## Current status

Before reaching for the history, ask what is in force **right now**:

- `/userinfo user:@member` — one embed with the member's full moderation status:
  banned, muted or timed out, active warn count, every active sanction with its ID,
  and the totals per type.
- `/ban list`, `/mute list`, `/timeout list`, `/warnings` — everything of that kind
  currently active on the server.
- `/ban info`, `/mute info`, `/timeout info`, `/warn info` — the full record of one
  sanction from its ID: who issued it, when, why, when it expires, and how it was
  closed.

`/userinfo` also surfaces disagreements between Discord and the sanction database —
a user banned on Discord with no recorded sanction, a leftover mute role, or a
timeout sanction Discord has already dropped.

---

## History

### In Discord

- `/userhistory user:@member` — everything that ever happened to that member.
- `/staffhistory moderator:@staff` — everything that staff member issued.

Both are paginated and ephemeral.

### In the dashboard

The **History** section shows the same data with filters, and lets you open a single
sanction to see its full detail — moderator, timestamps, reason, revocation — and
revoke it from there.

Every member also has a **profile page** reachable from the history, collecting their
sanctions in one place.

### Statuses

| Status | Meaning |
|---|---|
| **Active** | Currently in force |
| **Revoked** | Lifted early by a moderator |
| **Expired** | Ran out on its own (duration elapsed, or warn expiry reached) |
| **Closed** | Not applicable — a kick, which has nothing to lift |

---

## Automatic expiry

VionDefence sweeps for due sanctions **every 30 seconds** and lifts them:
temporary bans are unbanned, mutes have the role removed, warns are marked expired.
The member is notified by DM that the sanction ended, and the event is written to the
**Moderation** log category.

Expiries are processed while the bot is running. If the bot is offline when a sanction
comes due, it is lifted on the next sweep after it restarts.

---

Next: [Automod](automod.md)
