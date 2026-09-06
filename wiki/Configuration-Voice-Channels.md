# Configuration — Voice channels

**English** · [Italiano](IT-Configurazione-Canali-Vocali)

*Dashboard → your server → **Canali template** and **Canali privati***

Two separate systems. They look alike from outside and solve different problems.

| | Templated channels | Private channels |
|---|---|---|
| For | Generic overflow rooms | One personal room per member |
| Owner | Nobody | The member who opened it |
| Settings remembered | No | Yes, per member |
| Member controls | None | Rename, limit, privacy, trust, kick, ban |
| How many hubs | Many templates | One system per server |

Run both if you like — they use different hub channels.

---

## Templated channels

*Dashboard → **Canali template***

For "Gaming 1, Gaming 2, Gaming 3…" — rooms that appear when the previous one fills and
vanish when they empty. Nobody owns them.

### How it works

1. A member joins the template's **hub channel**.
2. A new voice channel appears in the template's **category**, named from the **name
   format**, with the template's **user limit**.
3. The member is moved into it.
4. It is deleted the moment the last person leaves.

### Creating a template

| Field | Meaning |
|---|---|
| **Category** | Where new channels are created |
| **Hub channel** | The voice channel members join to trigger creation |
| **Name format** | The naming pattern |
| **Max user count** | Limit on created channels. `0` = unlimited |

Placeholders for the name format:

| Placeholder | Becomes |
|---|---|
| `{id}` | An incrementing number, unique per template |
| `{username}` | The Discord username of whoever triggered it |
| `{displayname}` | Their server nickname, or username if they have none |

`Room {id}` gives *Room 1*, *Room 2*. `{displayname}'s room` gives *Marco's room*.

A hub channel belongs to exactly one template — reusing one is rejected.

You can also manage templates from Discord with `/channel-templates`. Note that
`/channel-templates clear` deletes every template with no confirmation step.

---

## Private channels

*Dashboard → **Canali privati***

For servers where each member should get a room they actually control.

### Setting it up

| Field | Meaning |
|---|---|
| **Enabled** | Turns the system on or off |
| **Hub channel** | The voice channel members join to get their room |
| **Category** | Where personal rooms are created |

Both the hub and the category are required before it can be enabled.

### What the member gets

They join the hub, and a room appears in the category with them as **owner**. Their
settings — name, user limit, privacy, trusted list, ban list — are remembered, so the
next room they open comes back the way they left it. The room is deleted when it empties;
the settings survive.

The default name is `House of {username}`; `{username}` and `{displayname}` both work.

### Privacy modes

| Mode | Who sees it | Who can join |
|---|---|---|
| **Free** | Everyone | Everyone |
| **Locked** | Everyone | Owner and trusted members |
| **Private** | Owner and trusted members | Owner and trusted members |

**Locked** is the one most people want: the room is visible, you can see who is inside,
but you cannot walk in uninvited.

### Owner controls

Available as buttons on the room's panel, and as `/voice` subcommands:

| Control | Effect |
|---|---|
| Rename | Changes the room name |
| Change limit | Sets the member cap, `0` removes it |
| Change privacy | Free / locked / private |
| Trust | Lets a specific member in while locked or private |
| Untrust | Revokes trust — does **not** remove someone already inside |
| Kick | Removes a member now |
| Ban | Blocks a member from joining, and revokes their trust |
| Unban | Lifts the ban — does **not** grant trust |
| Claim | Takes ownership, only if the previous owner has left |

**Claim** exists for orphaned rooms: the owner disconnects, other people are still in
there, and one of them takes over rather than being stuck. It is refused while the owner
is still present.

---

## Troubleshooting

| Symptom | Cause |
|---|---|
| No rooms are created | Bot lacks **Manage Channels** in the category |
| Rooms appear but the member stays in the hub | Bot lacks **Move Members** |
| Empty rooms are not deleted | Bot lost **Manage Channels**, or the channel was moved out of the category by hand |
| Privacy changes do nothing | Bot lacks **Manage Roles** / **Manage Channels** on the room |

The **Channel templates** and **Private channels** log categories carry the real error.
If you have not set them yet, see [Logs](Configuration-Logs).

---

Next: **[Tickets](Configuration-Tickets)**
