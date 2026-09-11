# Command reference

**English** · [Italiano](it/comandi.md)

Every VionDefence command is a Discord slash command. Replies are ephemeral —
only the person who ran the command sees them.

Commands are registered globally, so they appear in every server the bot is in, but
each server decides independently which ones are **enabled** and **who may run them**
(see [Permissions and restrictions](#permissions-and-restrictions)).

---

## Moderation

### `/kick`

Kicks a member from the server.

| Option | Required | Description |
|---|---|---|
| `user` | yes | The member to kick |
| `reason` | no | Reason, max 512 characters |

### `/ban add`

Bans a member. The ban can be permanent or temporary.

| Option | Required | Description |
|---|---|---|
| `user` | yes | The member to ban |
| `reason` | no | Reason, max 512 characters |
| `duration` | no | e.g. `10m`, `2h`, `3d`, `1w`. Leave empty for a permanent ban |

Temporary bans are lifted automatically when they expire.

### `/ban remove`

Unbans a member.

| Option | Required | Description |
|---|---|---|
| `user` | yes | The member to unban |
| `reason` | no | Reason for the unban |

### `/ban info`

Everything recorded about one ban: status, target, moderator, reason, when it was
issued, when it expires, and — if it is no longer active — when it was closed, by
whom, and why.

| Option | Required | Description |
|---|---|---|
| `ban-id` | yes | Sanction ID of the ban (from `/ban list`, `/userinfo` or `/userhistory`) |

The ID must belong to a **ban** issued **on this server**; anything else is reported
as not found.

### `/ban list`

Paginated list of every ban currently **active** on this server, newest first. Each
line carries the sanction ID, the target, the moderator, when it was issued, when it
expires and the reason.

### `/mute add`

Mutes a member using the server's **mute role** (configured in the dashboard under
Moderation). Fails if no mute role is set.

| Option | Required | Description |
|---|---|---|
| `user` | yes | The member to mute |
| `reason` | no | Reason, max 512 characters |
| `duration` | no | e.g. `30m`, `12h`, `2d`. Leave empty for an indefinite mute |

### `/mute remove`

Removes the mute role from a member.

| Option | Required | Description |
|---|---|---|
| `user` | yes | The member to unmute |
| `reason` | no | Reason for the unmute |

### `/mute info`

Everything recorded about one mute, in the same layout as `/ban info`.

| Option | Required | Description |
|---|---|---|
| `mute-id` | yes | Sanction ID of the mute |

### `/mute list`

Paginated list of every mute currently **active** on this server.

### `/timeout add`

Applies a **native Discord timeout**. Discord caps timeouts at 28 days.

| Option | Required | Description |
|---|---|---|
| `user` | yes | The member to time out |
| `duration` | yes | e.g. `10m`, `2h`, `3d` — max 28 days |
| `reason` | no | Reason, max 512 characters |

### `/timeout remove`

Removes an active timeout.

| Option | Required | Description |
|---|---|---|
| `user` | yes | The member to untimeout |
| `reason` | no | Reason |

### `/timeout info`

Everything recorded about one timeout, in the same layout as `/ban info`.

| Option | Required | Description |
|---|---|---|
| `timeout-id` | yes | Sanction ID of the timeout |

### `/timeout list`

Paginated list of every timeout currently **active** on this server.

### `/warn add`

Warns a member. Warns accumulate and can trigger automatic escalation —
see [Moderation](moderation.md#warn-escalation).

| Option | Required | Description |
|---|---|---|
| `user` | yes | The member to warn |
| `reason` | yes | Reason, max 512 characters |

### `/warn remove`

Removes a single active warn by its ID. Get the ID from `/warnings`, `/userinfo`
or `/userhistory`.

| Option | Required | Description |
|---|---|---|
| `warn-id` | yes | The ID of the warn to remove |
| `reason` | no | Reason for the removal |

### `/warn clear`

Removes **all** active warns from a member at once.

| Option | Required | Description |
|---|---|---|
| `user` | yes | The member whose warns to clear |
| `reason` | no | Reason for the removal |

### `/warn info`

Everything recorded about one warn, in the same layout as `/ban info`.

| Option | Required | Description |
|---|---|---|
| `warn-id` | yes | Sanction ID of the warn (from `/warnings` or `/userinfo`) |

### `/bulkdelete`

Deletes the most recent messages of the channel it is run in, optionally only those
sent by one member. Requires the **Basic** plan.

| Option | Required | Description |
|---|---|---|
| `user` | no | Only delete the messages sent by this member |
| `count` | no | How many messages to delete, from 1 to 100 |

What gets deleted depends on which options you pass:

| Options given | Effect |
|---|---|
| none | the last **100** messages of the channel |
| `count` only | the last `count` messages of the channel |
| `user` only | the last **50** messages of that member |
| `user` and `count` | the last `count` messages of that member |

The command always acts on **the channel it was run in**, never on the whole server.
When filtering by member, VionDefence reads back at most the last 1000 messages of
that channel looking for theirs.

Discord does not allow bulk deletion of messages older than **14 days**: those are
left untouched, and the reply says how many were skipped.

VionDefence needs **Manage Messages** and **Read Message History** in the channel.

---

## Duration syntax

Every `duration` option uses the same compact format:

| Unit | Meaning |
|---|---|
| `s` | seconds |
| `m` | minutes |
| `h` | hours |
| `d` | days |
| `w` | weeks |

Units can be combined and are summed: `1d12h` is 36 hours, `1w2d` is 9 days.
An invalid or zero duration is rejected with an error message.

---

## Status and active sanctions

### `/userinfo`

The current state of a user in one embed: account age, when they joined, their roles,
whether they are **banned**, **muted** or **timed out** right now, how many active
warns they carry, the list of their active sanctions with IDs, and the totals per
sanction type.

| Option | Required | Description |
|---|---|---|
| `user` | yes | The member to inspect |

Use it when you need the current picture rather than the full log: `/userhistory`
lists everything that ever happened, `/userinfo` answers "what is going on with this
user right now". It also works on users who already left or were banned.

The embed flags the cases where Discord and the sanction database disagree — someone
banned on Discord with no recorded sanction, a lingering mute role, or a timeout
sanction Discord is no longer applying — so those can be fixed instead of silently
drifting.

On servers running the [level system](levels.md) the embed also carries a **Level**
field: the level, the total XP, the rank and the XP missing for the next level. Where
the system is off the field is left out entirely, rather than showing an empty ladder.

Its color follows the per-sanction colors configured in the dashboard, picking the
most severe sanction still active on the user.

### `/warnings`

Paginated list of every warn currently **active** on this server. This is the
server-wide counterpart of the per-user warn count shown by `/userinfo`.

---

## History

### `/userhistory`

Shows the full sanction history of a member — every kick, ban, mute, timeout and warn,
with its ID, status (active, revoked, expired, closed), reason and moderator.

| Option | Required | Description |
|---|---|---|
| `user` | yes | The member whose history to view |

### `/staffhistory`

Shows the sanctions **issued by** a staff member. Useful for auditing your own team.

| Option | Required | Description |
|---|---|---|
| `moderator` | yes | The staff member to audit |

Both commands paginate their results.

---

## Temporary voice channels

### `/channel-templates new`

Creates a template. Members who join the hub channel get a new voice room in the
chosen category.

| Option | Required | Description |
|---|---|---|
| `discord-category` | yes | Category where new channels are created |
| `hub-channel` | yes | Voice channel members join to trigger creation |
| `channel-name-format` | yes | Name pattern, e.g. `Room {id}` or `{username}'s room` |
| `max-user-count` | no | User limit for created channels. `0` = unlimited |

Available placeholders in `channel-name-format`: `{id}`, `{username}`, `{displayname}`.

### `/channel-templates list`

Lists every template with its ID, category, hub channel, name format and user limit.
Paginated.

### `/channel-templates remove`

Deletes one template.

| Option | Required | Description |
|---|---|---|
| `template-id` | yes | The template ID, from `/channel-templates list` |

### `/channel-templates clear`

Deletes **all** templates on the server. There is no confirmation step.

---

## Private voice channel controls

`/voice` is the member-facing command for the room they own. Every subcommand opens a
modal or a selector — none of them take options directly.

| Subcommand | What it does |
|---|---|
| `/voice rename` | Renames your room |
| `/voice change-limit` | Sets the member limit, or `0` to reset it |
| `/voice change-privacy` | Switches between **free**, **locked** and **private** |
| `/voice trust` | Lets a specific member in while the room is locked or private |
| `/voice untrust` | Revokes trust (does **not** kick the member out) |
| `/voice kick` | Removes a member from your room |
| `/voice ban` | Bans a member from your room (removes trust if they had it) |
| `/voice unban` | Lifts that ban (does **not** grant trust) |
| `/voice claim` | Takes ownership of the room if the previous owner has left it |

The same actions are available as buttons on the room's control panel — see
[Voice channels](voice-channels.md).

---

## Tickets

`/ticket` only works **inside a ticket channel**.

| Subcommand | Options | What it does |
|---|---|---|
| `/ticket close` | — | Closes this ticket |
| `/ticket claim` | — | Assigns this ticket to you |
| `/ticket release` | — | Releases a ticket you claimed |
| `/ticket add` | `user` | Adds a member to this ticket |
| `/ticket remove` | `user` | Removes a member from this ticket |
| `/ticket move` | `panel` | Moves the ticket to another panel's category |

See [Tickets](tickets.md) for how panels, teams and transcripts work.

---

## Levels and promotion

### `/level`

The level card of a member: their level out of the last one, their total XP, their
rank on the server, and a progress bar towards the next level with the XP still
missing. The footer counts the messages and the voice minutes that got them there.

| Option | Required | Description |
|---|---|---|
| `user` | no | The member to look up. Defaults to whoever ran the command |

Answers that the system is disabled on servers where the level system is off, and
refuses bots, which never earn XP. See [Level system](levels.md).

### `/server stats`

Member, bot and staff counts for this server, as an ephemeral reply only you see.
Recalculates on the spot rather than reading the counter channels, and adds how many
of those members and staff are **online**.

Takes no options. Works with or without the counter channels turned on — see
[Member counters](counters.md).

### `/bump`

Puts this server in the **bot's own Discord description** — name and invite link — for
a window drawn at random between 12 and 24 hours.

Takes no options: what gets written is set once in the dashboard.

Only **one server at a time per region** can hold the slot: the description belongs
to the bot of that region. While it is
taken, the command answers with when it frees up. Running it can also pay XP, if the
dashboard sets a reward and the level system is on.

Requires the **Basic** plan. See [Bump ME](bump.md).

---

## Utility

### `/ping`

Returns your latency with the bot in milliseconds.

**Disabled by default** — enable it in the dashboard under **Commands** if you want it.

---

## Permissions and restrictions

Every command has four independent settings in the dashboard's **Commands** section:

| Setting | Effect |
|---|---|
| **Enabled** | Turn the command off entirely on this server |
| **Permission** | The Discord permission a member must hold to run it |
| **Roles** | If non-empty, only these roles may run it |
| **Channels** | If non-empty, the command only works in these channels |

Roles and channels are **allowlists**: leaving them empty means "no restriction".
The checks are combined with AND — if you set both a permission and a role list, a
member needs the permission **and** one of the roles. Setting the permission to
*none* disables the permission check entirely.

### Defaults

| Command | Enabled | Required permission |
|---|---|---|
| `/kick` | yes | Kick Members |
| `/ban` | yes | Ban Members |
| `/warn` | yes | Moderate Members |
| `/mute` | yes | Moderate Members |
| `/timeout` | yes | Moderate Members |
| `/userinfo` | yes | Moderate Members |
| `/warnings` | yes | Moderate Members |
| `/userhistory` | yes | Moderate Members |
| `/staffhistory` | yes | Moderate Members |
| `/bulkdelete` | yes | Manage Messages |
| `/channel-templates` | yes | Manage Channels |
| `/voice` | yes | none — everyone |
| `/level` | yes | none — everyone |
| `/server` | yes | none — everyone |
| `/bump` | yes | none — everyone |
| `/ticket` | yes | none — everyone |
| `/ping` | **no** | none — everyone |

### Safety rules that always apply

Regardless of configuration, VionDefence refuses to:

- let a moderator sanction **themselves**;
- let anyone sanction **the bot**;
- act on a member who sits **above the bot** in the role hierarchy — Discord would
  reject the action anyway.

---

Next: [Moderation](moderation.md)
