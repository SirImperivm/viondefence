# Installation

**English** · [Italiano](IT-Installazione)

Inviting the bot, giving it what it needs, and getting into the dashboard.

---

## 1. Invite the bot

Open [viondefence.com](https://viondefence.com) and use the **Add the bot** button.
Discord will ask which server to install it on, and will only list servers where you
hold **Manage Server**.

Accept the permissions Discord proposes. Each one is there for a reason:

| Permission | Without it |
|---|---|
| **Manage Channels** | No temporary voice channels, no ticket channels |
| **Manage Roles** | Mutes fail, ticket permissions cannot be written |
| **Kick Members** | `/kick` and the automod kick action fail |
| **Ban Members** | `/ban` fails, and temporary bans never lift |
| **Moderate Members** | `/timeout` fails |
| **Move Members** | Voice rooms get created but members are never moved into them |
| **Send Messages / Embed Links** | No log embeds, no ticket panels |
| **Read Message History** | Ticket transcripts come out empty |

You can grant fewer, and the rest of the bot keeps working — the affected feature is
the only thing that breaks. It breaks *silently* from a member's point of view, though;
the error goes to the **General** log category, which is one more reason to
[set up logging early](Configuration-Logs).

---

## 2. Fix the role hierarchy

This is the step people skip, and then spend an hour debugging.

Open **Server Settings → Roles** and drag the **VionDefence** role high up — above
every role it will need to act on.

Discord enforces two rules that no permission can override:

- a bot cannot kick, ban, mute or time out anyone whose highest role sits **above** its
  own;
- a bot cannot **assign** a role that sits above its own.

So if your mute role ends up above VionDefence, every `/mute` fails. If your
moderators sit above VionDefence, automod can never act on them — which is sometimes
what you want, and is what the *Respect role hierarchy* option in
[Automod](Configuration-Automod) is for.

A safe position: directly under your admin roles, above everything else.

---

## 3. Open the dashboard

Go to [viondefence.com/dashboard](https://viondefence.com/dashboard) and log in
with Discord.

You will see every server where **both** are true:

- you hold **Manage Server**, and
- VionDefence is installed.

Click one to open its configuration panel. The sidebar lists the sections; each has its
own page in this wiki.

### If your server is missing from the list

| Cause | Fix |
|---|---|
| The bot is not on that server | Re-run step 1 and pick it |
| You do not hold Manage Server | Ask the owner to grant it, or to do the setup |
| Your Discord session is stale | Log out of the dashboard and back in — this is the common one |

---

## 4. Check the commands arrived

In Discord, type `/` in any channel. You should see the VionDefence commands.

Slash commands are registered **globally**, so the first time they can take a few
minutes to propagate. If they still do not appear after that, re-invite the bot and
make sure the `applications.commands` scope is included in the invite — an invite with
only the `bot` scope installs the bot without its commands.

---

## Accounts and linking

You can sign in with Discord, or with an email and password, and link the two so either
works. That lives under **Account → Access** and is unrelated to any single server.

Plans are attached to a specific server, and are managed from **Account →
Subscriptions**. Which features and limits a server gets — how many voice templates,
how many ticket panels, which log categories — depends on that plan. Current plans:
[viondefence.com/pricing](https://viondefence.com/pricing).

---

Next: **[General configuration](Configuration-General)**
