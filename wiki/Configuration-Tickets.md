# Configuration — Tickets

**English** · [Italiano](IT-Configurazione-Ticket)

*Dashboard → your server → **Ticket***

The ticket system is built around **panels**. A panel is one kind of request — support,
reports, applications — with its own category, its own team, its own opening form and
its own rules.

---

## The flow

1. You create one or more **panels**.
2. VionDefence posts a **panel message** with a selector listing them.
3. A member picks one. If it has a form, they fill it in a popup.
4. A private channel appears in that panel's category, visible to the member and the
   panel's teams.
5. Support claims it, handles it, closes it. A transcript is filed.

---

## Panel settings

| Setting | Meaning |
|---|---|
| **Name** | Shown in the selector, and used by `/ticket move` |
| **Description** | Sub-label in the selector |
| **Emoji** | Icon in the selector |
| **Position** | Sort order |
| **Enabled** | Hides the panel without deleting it |
| **Category** | Where ticket channels are created |
| **Log channel** | Where this panel's events and transcripts go |
| **Ticket name template** | Naming pattern for ticket channels |
| **User team** | Who may open a ticket here |
| **Support team** | Who handles them |
| **Admin team** | Elevated staff for this panel |
| **Allow user close** | Whether the opener may close their own ticket |
| **Transcript required (support)** | Force a transcript when support closes |
| **Transcript required (admin)** | Force a transcript when an admin closes |
| **Form fields** | The questions asked on opening |

### Ticket name template

Default `ticket-{id}`. Placeholders: `{id}` (the panel's own incrementing number),
`{username}`, `{displayname}`.

The result is lowercased, spaces become hyphens, and it is trimmed to 100 characters —
Discord's rules for channel names.

---

## Teams — the part to get right

Each team is a set of roles and/or users.

| Team | Can |
|---|---|
| **User team** | Open a ticket on this panel |
| **Support team** | See, claim, release and close tickets; add and remove members |
| **Admin team** | All of the above, plus release a ticket someone else claimed |

**The user team behaves differently from the other two.** Leave it **empty** and
*everyone* can open tickets on that panel — empty means no restriction. Fill it to make
a panel staff-only, or restricted to a subscriber role.

The support and admin teams do **not** work that way. An empty support team means
**nobody** can claim or close tickets on that panel, and it will silently pile up
unanswered tickets. Always set at least one.

---

## Claiming

A support member claims a ticket to signal they are on it. While claimed, the other
support members lose write access to that channel — so the conversation stays between
the opener and one handler instead of becoming a crowd.

- **Claim** — the button, or `/ticket claim`. Refused if someone already holds it.
- **Release** — the button, or `/ticket release`. Only the claimer or an **admin team**
  member can release.

---

## The opening form

A panel can ask questions before creating the ticket. Each field has a **label**, a
**type** (`text` or `file`), a **required** flag, an optional **placeholder**, and
optional **min/max length** for text.

Answers are posted into the ticket channel on open, so support has the context
immediately. A panel with no fields opens the ticket straight away.

Keep forms short. Three good questions get answered; eight get abandoned.

---

## Transcripts

Closing opens a popup asking for an optional **reason** (max 500 characters).

Whether a transcript is produced depends on the panel:

- **Transcript required** for the closer's role → always generated, no opt-out.
- **Not required** → the popup shows a **Save transcript** checkbox, ticked by default.
  The closer can untick it.

The two toggles are independent, so you can force transcripts on support closes while
letting admins close quietly, or the reverse.

The transcript is a self-contained **HTML file**, `transcript-ticket-<number>.html`,
posted to the panel's **log channel** along with who closed the ticket.

> Transcripts go to the **panel's** log channel, not to the **Tickets** log category.
> The category gets the events — opened, claimed, closed. Set both.

---

## Who can close

| Closer | Allowed |
|---|---|
| The opener | Only if **Allow user close** is on |
| Support team | Yes |
| Admin team | Yes |
| Anyone else | No |

---

## Managing tickets from Discord

Inside a ticket channel: `/ticket claim`, `/ticket release`, `/ticket add`,
`/ticket remove`, `/ticket move panel:<name>`, `/ticket close`.

`/ticket move` is for tickets opened on the wrong panel — it re-files them under the
right team and category without losing the conversation.

---

## Troubleshooting

| Symptom | Cause |
|---|---|
| The selector is empty | Every panel is disabled, or the member is in no panel's user team |
| Ticket channels are not created | Bot lacks **Manage Channels** in the category or **Manage Roles** |
| No transcript arrives | Panel log channel unset, deleted, or the bot cannot attach files there |
| Support cannot see new tickets | Support team is empty, or its roles were deleted |

---

Next: **[Automod](Configuration-Automod)**
