# Tickets

**English** · [Italiano](it/ticket.md)

A ticket system built around **panels**. Each panel is one kind of request — support,
reports, applications — with its own category, its own team, its own open form and its
own rules.

Configure it in the dashboard under **Tickets**.

---

## How it works

1. You create one or more **panels** in the dashboard.
2. VionDefence posts a **ticket panel message** with a selector listing them.
3. A member picks a panel. If the panel has a form, they fill it in a modal.
4. A private channel is created in the panel's category, visible to the member and the
   panel's teams.
5. Support claims it, handles it, closes it. A transcript is filed.

---

## Panel settings

| Setting | Meaning |
|---|---|
| **Name** | Shown in the selector, and used by `/ticket move` |
| **Description** | Sub-label in the selector |
| **Emoji** | Icon in the selector |
| **Position** | Sort order in the selector |
| **Enabled** | Hides the panel from the selector without deleting it |
| **Category** | Where ticket channels are created |
| **Log channel** | Where this panel's ticket events and transcripts are sent |
| **Ticket name template** | Naming pattern for ticket channels |
| **User team** | Who may open a ticket on this panel |
| **Support team** | Who handles tickets on this panel |
| **Admin team** | Elevated staff for this panel |
| **Allow user close** | Whether the person who opened it may close it |
| **Transcript required (support)** | Force a transcript when support closes |
| **Transcript required (admin)** | Force a transcript when an admin closes |
| **Form fields** | The questions asked when opening |

### Ticket name template

Default: `ticket-{id}`.

| Placeholder | Replaced with |
|---|---|
| `{id}` | The panel's ticket number, incrementing per panel |
| `{username}` | The opener's Discord username |
| `{displayname}` | Their nickname on this server |

The result is lowercased, spaces become hyphens, and it is trimmed to 100 characters —
Discord's channel name rules.

---

## Teams

Each team is a set of **roles** and/or **users**.

| Team | Can |
|---|---|
| **User team** | Open a ticket on this panel |
| **Support team** | See, claim, release, close tickets; add and remove members |
| **Admin team** | Everything support can, plus release a ticket claimed by someone else |

**Leave the user team empty to let everyone open tickets** on that panel — an empty
user team means "no restriction". Fill it to make a panel staff-only, or restricted to
a subscriber role.

Support and admin teams are not "empty means everyone" — an empty support team means
nobody can claim or close tickets on that panel. Always set at least one.

---

## Claiming

A support member claims a ticket to signal they are handling it. While claimed, the
other support members lose write access to that channel — the conversation stays
between the opener and one handler instead of turning into a crowd.

- **Claim** — `/ticket claim` or the **Claim** button. Refused if someone already
  claimed it.
- **Release** — `/ticket release` or the **Release** button. Only the claimer or an
  **admin team** member can release.

---

## The open form

A panel can ask questions before the ticket is created. Each field has:

| Property | Meaning |
|---|---|
| **Label** | The question |
| **Type** | `text` or `file` |
| **Required** | Whether it can be left blank |
| **Placeholder** | Hint text inside the input |
| **Min / max length** | Length bounds for text fields |

Answers are posted in the ticket channel when it opens, so support sees the context
immediately.

Panels with no form fields open the ticket straight away.

---

## Closing and transcripts

Closing opens a modal asking for an optional **reason** (max 500 characters).

Whether a transcript is produced depends on the panel:

- **Transcript required** for the closer's role → a transcript is always generated;
  there is no opt-out.
- **Not required** → the modal shows a **Save transcript** checkbox, ticked by default.
  The closer can untick it to close without one.

The two *transcript required* toggles are independent, so you can force transcripts
for support closes while letting admins close quietly, or the other way round.

The transcript is a self-contained **HTML file** named
`transcript-ticket-<number>.html`, posted to the panel's **log channel** together with
who closed the ticket. Ticket events are also written to the **Tickets** log category —
see [Logs](logs.md).

### Who can close

| Closer | Allowed |
|---|---|
| The person who opened it | Only if **Allow user close** is on for that panel |
| Support team | Yes |
| Admin team | Yes |
| Anyone else | No |

---

## Managing a ticket

From inside the ticket channel:

| Command | Effect |
|---|---|
| `/ticket claim` | Assign it to yourself |
| `/ticket release` | Hand it back to the pool |
| `/ticket add user:@member` | Pull someone into the ticket |
| `/ticket remove user:@member` | Remove them again |
| `/ticket move panel:<name>` | Move the ticket to another panel's category |
| `/ticket close` | Close it |

`/ticket move` is for tickets opened on the wrong panel — it re-files them under the
right team without losing the conversation.

---

## Troubleshooting

**The selector shows no panels.** Every panel is disabled, or the member is not in any
panel's user team.

**Ticket channels are not created.** VionDefence needs **Manage Channels** in the
panel's category and **Manage Roles** to write the permission overwrites.

**No transcript arrives.** The panel's log channel is unset, deleted, or the bot cannot
send attachments in it.

**Support cannot see new tickets.** The support team is empty, or the roles in it were
deleted.

---

Next: [Logs](logs.md)
