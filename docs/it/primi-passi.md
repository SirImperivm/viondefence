# Primi passi

[English](../getting-started.md) · **Italiano**

Tre passaggi e circa due minuti per avere VionDefence operativo sul tuo server.

---

## 1. Aggiungi il bot al server

Usa il pulsante **Aggiungi il bot** sul [sito](https://viondefence.com) e scegli il
server su cui installarlo.

Ti serve il permesso **Gestire il server** su quel server — Discord elenca solo i
server su cui ce l'hai.

Durante l'invito lascia i permessi che Discord propone. A VionDefence servono per
funzionare:

| Permesso | Serve per |
|---|---|
| Gestire i canali | Creare ed eliminare canali vocali temporanei e canali dei ticket |
| Gestire i ruoli | Applicare il ruolo mute, i permessi dei canali ticket |
| Espellere / Bannare membri | `/kick`, `/ban`, azioni attive dell'automod |
| Modera membri | `/timeout` e i timeout dell'automod |
| Spostare membri | Spostare il membro nel canale vocale appena creato |
| Leggere la cronologia / Inviare messaggi / Incorporare link | Embed di log, pannelli ticket, transcript |

> Se in seguito togli uno di questi permessi, la funzione collegata smette di
> funzionare senza che il membro se ne accorga — l'errore finisce nella categoria di
> log **Generale**. Vedi [Log](log.md).

---

## 2. Apri la dashboard

Vai su https://viondefence.com/dashboard e accedi con Discord.

Vedrai tutti i server su cui hai **Gestire il server** e su cui VionDefence è
installato. Clicca su uno per aprirne il pannello di configurazione.

Se un server non compare nell'elenco:

- il bot non è installato lì, oppure
- non hai Gestire il server su quel server, oppure
- la sessione Discord è vecchia — esci e rientra.

---

## 3. Imposta le basi

Apri per prima cosa la sezione **Generale** e imposta:

- **Lingua** — `Italiano (it-IT)` o `English (en-US)`. È la lingua di tutti i messaggi
  che il bot invia *in quel server*, indipendente dalla lingua della dashboard.
- **Fuso orario** — usato per ogni timestamp in log, transcript e cronologia
  (es. `Europe/Rome`).
- **Formato data** e **Formato ora** — come vengono scritti quei timestamp
  (es. `DD/MM/YYYY` e `HH:mm:ss`).

I valori predefiniti sono `en-US`, `America/New_York`, `MM/DD/YYYY`, `hh:mm:ss A`.

---

## 4. Poi configura quello che ti serve davvero

Nient'altro è attivo di default. Scegli i moduli che vuoi:

| Voglio… | Vai su | Guida |
|---|---|---|
| Un registro di quello che fa il bot | **Log** | [Log](log.md) |
| Kick/ban/warn/mute con cronologia | **Moderazione** | [Moderazione](moderazione.md) |
| Filtro automatico di spam / link / insulti | **Automod** | [Automod](automod.md) |
| Che i membri abbiano la loro stanza vocale | **Canali template** | [Canali vocali](canali-vocali.md) |
| Un sistema di ticket di assistenza | **Ticket** | [Ticket](ticket.md) |
| Limitare chi può usare quali comandi | **Comandi** | [Comandi](comandi.md#permessi-e-restrizioni) |

Su un server nuovo un ordine sensato è: **Generale → Log → Moderazione → Comandi**, poi
i moduli opzionali.

---

## Una nota sul ruolo mute

Sia `/mute` sia l'azione `mute` dell'automod hanno bisogno di un **ruolo mute**
configurato in **Moderazione**. Finché non ne imposti uno, quelle azioni falliscono.

Crea un ruolo su Discord (es. `Mutato`), negagli *Inviare messaggi*, *Parlare* e
*Aggiungere reazioni* nei tuoi canali, poi selezionalo nella dashboard. Assicurati che
il ruolo VionDefence stia **sopra** di esso nella lista dei ruoli, altrimenti il bot
non può assegnarlo.

---

Avanti: [Dashboard](dashboard.md)
