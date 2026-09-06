# Temporary voice channels

**English** · [Italiano](it/canali-vocali.md)

VionDefence has two separate systems for on-demand voice rooms. They look similar
from the outside but do different jobs.

| | Templated channels | Private channels |
|---|---|---|
| Purpose | Generic overflow rooms | One personal room per member |
| Owner | Nobody | The member who created it |
| Settings survive | No | Yes — remembered for next time |
| Member controls | None | Full: rename, limit, privacy, trust, kick, ban |
| Number of hubs | Many templates | One system per server |

Use **templated channels** for "Gaming 1, Gaming 2, Gaming 3…" style overflow.
Use **private channels** when each member should get a room they actually own.

You can run both at once — they use different hub channels.

---

## Templated channels

Configure them in the dashboard under **Templated channels**, or with
[`/channel-templates`](commands.md#temporary-voice-channels).

### How it works

1. A member joins the template's **hub channel**.
2. VionDefence creates a new voice channel in the template's **category**, named
   from the **name format**, with the template's **user limit**.
3. The member is moved into it.
4. When the last person leaves, the channel is deleted.

### Settings

| Setting | Meaning |
|---|---|
| **Category** | Where new channels are created |
| **Hub channel** | The voice channel members join to trigger creation |
| **Name format** | The name pattern for new channels |
| **Max user count** | User limit on created channels. `0` = unlimited |

### Name format placeholders

| Placeholder | Replaced with |
|---|---|
| `{id}` | An incrementing number, unique per template |
| `{username}` | The Discord username of the member who triggered it |
| `{displayname}` | Their nickname on this server, or username if none |

Examples: `Room {id}` → `Room 1`, `Room 2`… · `{displayname}'s room` → `Marco's room`.

You can create as many templates as your plan allows, each with its own hub.

> A hub channel can only belong to one template. Trying to reuse one is rejected.

---

## Private channels

Configure them in the dashboard under **Private channels**.

### Settings

| Setting | Meaning |
|---|---|
| **Enabled** | Turns the whole system on or off |
| **Hub channel** | The voice channel members join to get their room |
| **Category** | Where personal rooms are created |

Both the hub channel and the category are **required** to enable the system.

### How it works

A member joins the hub and gets their own room, created in the category. They are its
**owner**, and VionDefence remembers their settings — name, user limit, privacy,
trusted list, ban list — so the next room they open comes back the way they left it.

The default room name is `House of {username}`; `{username}` and `{displayname}` are
both available as placeholders.

The room is deleted when it empties, but the owner's settings persist.

### Privacy modes

| Mode | Who can see it | Who can join |
|---|---|---|
| **Free** | Everyone | Everyone |
| **Locked** | Everyone | The owner and trusted members only |
| **Private** | The owner and trusted members only | The owner and trusted members only |

**Locked** is the useful middle ground: people can see the room exists and who is in
it, but cannot walk in.

### Owner controls

The owner drives their room either with the [`/voice`](commands.md#private-voice-channel-controls)
command or with the button panel VionDefence posts for the room.

| Control | Effect |
|---|---|
| **Rename** | Changes the room name |
| **Change limit** | Sets the member cap, `0` to remove it |
| **Change privacy** | Switches between free / locked / private |
| **Trust** | Lets a specific member in while locked or private |
| **Untrust** | Revokes trust. Does **not** remove them if they are already inside |
| **Kick** | Removes a member from the room now |
| **Ban** | Blocks a member from joining. Also revokes their trust |
| **Unban** | Lifts the ban. Does **not** grant trust |
| **Claim** | Takes ownership, only if the previous owner has left the room |

Trust and ban lists are stored per owner and reused across sessions.

**Claim** exists for the case where the owner disconnects and leaves other people
behind in an orphaned room — one of them takes over instead of the room becoming
uncontrollable. It is refused while the owner is still inside.

---

## Troubleshooting

**Rooms are not being created.** Check that VionDefence has **Manage Channels** in
the target category and **Move Members** on the server. Check the **Channel
templates** / **Private channels** log categories for the actual error.

**Rooms are created but the member stays in the hub.** The bot is missing
**Move Members**.

**Rooms are not deleted when empty.** The bot lost **Manage Channels** on the category
after the room was created, or the channel was moved out of the category manually.

**Privacy changes have no effect.** The VionDefence role must be able to edit
permission overwrites on the room — it needs **Manage Roles** and **Manage Channels**.

---

Next: [Tickets](tickets.md)
