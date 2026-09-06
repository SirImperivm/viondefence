# Primi passi

[English](Getting-Started) · **Italiano**

Prima di invitare qualsiasi cosa, cinque minuti di contesto perché il resto della wiki
abbia senso.

---

## Cos'è VionDefence

Un bot Discord che gestisce moderazione, ticket, canali vocali temporanei e filtri
automatici dei contenuti — configurato da una **dashboard web** invece che da una lunga
lista di comandi slash.

I comandi slash esistono comunque, e lo staff li usa tutti i giorni. Ma la configurazione
avviene nel browser, e non devi insegnare al tuo team la sintassi di un comando per
cambiare un'impostazione.

---

## Cosa ti serve

| Requisito | Perché |
|---|---|
| Un server Discord | Ovviamente |
| Il permesso **Gestire il server** | Discord ti lascia installare bot solo dove ce l'hai, e la dashboard elenca solo i server dove ce l'hai |
| Qualche minuto | La configurazione di base è davvero breve |

**Non** ti serve un database, un hosting o alcuna competenza tecnica: VionDefence è un
servizio ospitato.

---

## Come si incastrano i pezzi

```
Server Discord  ──►  Bot VionDefence  ──►  log, sanzioni, ticket, stanze vocali
       ▲                      ▲
       │                      │
  i tuoi membri          tu, dalla
  usano i comandi        dashboard
```

Tre cose valgono la pena di essere capite subito:

**1. La configurazione è per server.** Ogni impostazione di cui leggerai vive su un
singolo server Discord. Se ne gestisci tre, configuri tre volte. Anche il piano è
associato al singolo server.

**2. La lingua del bot è separata dalla tua.** La dashboard segue la tua preferenza
personale. La lingua che il bot *parla in un server* è un'impostazione del server. Un
admin italiano può benissimo gestire un server anglofono.

**3. Niente è attivo di default.** Appena installato, nessuna categoria di log ha un
canale, nessun modulo automod è acceso, non esiste nessun template vocale e non c'è un
ruolo mute. È voluto: il bot non tocca il tuo server finché non glielo dici. L'unica
eccezione sono i comandi slash, attivi da subito con permessi predefiniti sensati.

---

## L'ordine che funziona

Seguire questo ordine evita i due problemi più comuni — configurare alla cieca, e i mute
che falliscono in silenzio:

1. **[Installa il bot](IT-Installazione)** e apri la dashboard.
2. **[Generale](IT-Configurazione-Generale)** — lingua, fuso orario, formato data. Fallo
   per primo: ogni timestamp che vedrai dopo dipende da qui.
3. **[Log](IT-Configurazione-Log)** — dai un canale almeno a *Moderazione* e *Generale*.
   Da quel momento vedi cosa sta facendo il bot e perché qualcosa è fallito.
4. **[Moderazione](IT-Configurazione-Moderazione)** — il ruolo mute, e la gerarchia dei
   ruoli che lo fa funzionare.
5. **[Comandi](IT-Configurazione-Comandi)** — verifica che i permessi predefiniti
   corrispondano ai ruoli del tuo staff.

Poi, quando ti servono davvero:

- **[Canali vocali](IT-Configurazione-Canali-Vocali)** — stanze vocali su richiesta.
- **[Ticket](IT-Configurazione-Ticket)** — il sistema di assistenza.
- **[Automod](IT-Configurazione-Automod)** — i filtri automatici. Leggi la pagina prima
  di accendere qualcosa: c'è un modo giusto di attivarli.

---

## Due parole sui permessi

Quasi tutte le segnalazioni "il bot non funziona" si riducono a una di queste tre cose:

- un **permesso Discord** che manca al bot;
- la **gerarchia dei ruoli** — il bot non può agire su chi sta sopra di lui, né assegnare
  un ruolo più in alto del proprio;
- un **canale di log** mai impostato, quindi l'errore è invisibile.

La pagina [Installazione](IT-Installazione) copre i primi due come si deve. Imposta
subito i log e il terzo smette di essere un problema.

---

Avanti: **[Installazione](IT-Installazione)**
