# FAQ & troubleshooting

**English** · [Italiano](it/faq.md)

---

## Setup

**My server does not appear in the dashboard.**
Three possible causes: VionDefence is not installed on it, you do not have **Manage
Server** on it, or your Discord session is stale. Log out and back in first — it is the
common one.

**I invited the bot but no commands show up.**
Commands are registered globally and can take a few minutes to propagate the first
time. If they still do not appear, re-invite the bot making sure the
`applications.commands` scope is included.

**A command says it is not enabled.**
It is switched off for that server. Turn it on in the dashboard under **Commands**.
`/ping` is off by default.

**A command says I lack permission.**
Check the command's row under **Commands**: it may require a Discord permission you do
not hold, a role you are not in, or it may be restricted to specific channels. All
three checks apply together.

---

## Moderation

**`/mute` fails.**
Almost always one of two things:

1. No mute role is set in **Moderation**. Set one.
2. The mute role sits **above** the VionDefence role in Server Settings → Roles.
   A bot cannot assign a role above its own. Drag VionDefence above it.

**I cannot sanction a specific member.**
VionDefence refuses to act on anyone ranked above it in the role hierarchy, on
itself, and on the moderator running the command. Move the VionDefence role higher
if the target is genuinely below you but above the bot.

**A temporary ban did not lift.**
Expiries are swept every 30 seconds while the bot is online. If the bot was offline
when it came due, it lifts shortly after it restarts. If it is still stuck, check that
the bot still has **Ban Members**.

**A warn escalation rule did not fire.**
Rules match the active warn count **exactly**. A rule at threshold 3 fires on the third
active warn only — if the member jumped from 2 to 4 because you also cleared and
re-added warns, it will not fire. Check the count in `/userhistory`, and remember that
expired and revoked warns are not active.

**Members are not getting DMs about their sanctions.**
Either the DM notification for that sanction type is off in **Moderation**, or the
member has DMs from server members disabled. The sanction still applies either way.

---

## Automod

**Automod is not catching anything.**
Check, in order: the module is **enabled**; the member is not in **exempt roles** or
**exempt users**; **respect role hierarchy** is not excluding them because they rank
above the bot. Bots and system messages are always ignored.

**Automod catches too much.**
For anti-insult, lower the **sensitivity**. For anti-advertising, add domains to
**whitelisted domains** or turn off **block links** while keeping **block Discord
invites**. For anti-flood, raise **max messages** or shorten the **interval**.

**Automod detects but does not sanction.**
The module is in **passive** mode. Switch it to **passive + active** and pick an
action. A `timeout` action with no duration is skipped.

**Insult detection is inconsistent.**
Raise **context messages** so the classifier sees more of the conversation, and run in
passive mode long enough to tune the sensitivity before enabling an action.

---

## Voice channels

**Rooms are not created when I join the hub.**
VionDefence needs **Manage Channels** in the destination category and **Move
Members** on the server. The **Channel templates** or **Private channels** log
categories will show the real error.

**Rooms are created but I stay in the hub.**
The bot is missing **Move Members**.

**Empty rooms are not deleted.**
The bot lost **Manage Channels** on the category, or the channel was manually moved out
of it.

**`/voice` says I do not own a channel.**
You are not in a private room you own. `/voice` works on the room you are currently
in, and only for its owner. If the owner left, use `/voice claim`.

**Privacy changes do nothing.**
The bot needs **Manage Roles** and **Manage Channels** to rewrite the room's permission
overwrites.

---

## Tickets

**The ticket selector is empty.**
Every panel is disabled, or you are not in any panel's **user team**. An empty user
team means everyone can open that panel — a non-empty one restricts it.

**Nobody can close or claim tickets.**
The panel's **support team** is empty, or the roles in it were deleted. An empty
support team locks the panel.

**I closed a ticket but got no transcript.**
Either the **Save transcript** checkbox was unticked in the close modal, or the panel's
**log channel** is unset, deleted, or unwritable by the bot.

**A ticket was opened on the wrong panel.**
`/ticket move panel:<name>` re-files it under the right team and category without
losing the conversation.

---

## Logs

**A category logs nothing.**
Its **channel** is empty — that is how a category is turned off. Set one.

**A category has a channel but still logs nothing.**
The channel was deleted, is not a text channel, the bot cannot send or embed there, or
the category is not included in the server's plan.

**Timestamps are in the wrong timezone.**
Set the timezone under **General**. It applies to logs, transcripts and history alike.

---

## Language

**The bot replies in the wrong language.**
The bot's language is a **per-server** setting under **General**, separate from your
own dashboard language. Change it there.

---

## Still stuck?

Reach us on the Discord support server or by email:
https://viondefence.com/contacts
