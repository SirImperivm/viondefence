# Configuration — Commands

**English** · [Italiano](IT-Configurazione-Comandi)

*Dashboard → your server → **Comandi***

One card per slash command. The toggle on the card switches the command on and off; the
**wrench** opens a popup form with the three access controls.

---

## The four controls

| Control | Where | Effect |
|---|---|---|
| **Enabled** | On the card | Turns the command off entirely on this server |
| **Permission** | In the popup | The Discord permissions a member must hold |
| **Roles** | In the popup | If non-empty, only these roles may run it |
| **Channels** | In the popup | If non-empty, the command only works in these channels |

Roles and channels are **allowlists**. Empty means no restriction — not "nobody".

The checks combine with **AND**. Set both a permission and a role list and a member needs
the permission *and* one of the roles. Clear every permission and the permission check is
skipped entirely.

Each of the three saves independently — there is a save button per block, and it only
lights up when you have actually changed something.

---

## Defaults

| Command | Enabled | Permission |
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
| `/channel-templates` | yes | Manage Channels |
| `/voice` | yes | none — everyone |
| `/ticket` | yes | none — everyone |
| `/ping` | **no** | none — everyone |

`/voice` and `/ticket` are open to everyone on purpose: they are member-facing, and
operate only on the member's own voice room or on the ticket channel they are standing
in.

Full option-by-option reference for every command:
[docs/commands.md](https://github.com/SirImperivm/viondefence/blob/master/docs/commands.md).

---

## Two ways to give staff access

**By permission** — the default. Anyone holding *Moderate Members* can warn. Simple, and
it tracks your existing Discord roles without extra work.

**By role** — add your `Moderator` role to the command's role list. Explicit, and it
survives someone rearranging Discord permissions.

Most servers are fine with the defaults. Reach for the role list when your Discord
permissions do not cleanly express who your moderators are.

---

## Restricting to channels

Adding channels is how you keep `/voice` out of general chat, or confine `/userhistory`
to the staff channel so member history is never pulled up in public.

Leave it empty unless you have that specific need — a channel list is one more thing to
update when you restructure the server.

---

## Safety rules you cannot switch off

Whatever you configure, VionDefence refuses to:

- let a moderator sanction **themselves**;
- let anyone sanction **the bot**;
- act on a member ranked **above the bot** in the role hierarchy.

The last one is Discord's rule, not the bot's. See
[Installation](Installation#2-fix-the-role-hierarchy).

---

## Do this now

1. Skim the list and confirm the default permissions match how your staff roles are set
   up.
2. Enable `/ping` if you want a latency check available.
3. Leave the role and channel lists empty unless you have a reason.

---

Next: **[Voice channels](Configuration-Voice-Channels)**
