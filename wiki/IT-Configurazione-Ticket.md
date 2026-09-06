# Configurazione — Ticket

[English](Configuration-Tickets) · **Italiano**

*Dashboard → il tuo server → **Ticket***

Il sistema di ticket è costruito attorno ai **pannelli**. Un pannello è un tipo di
richiesta — assistenza, segnalazioni, candidature — con la sua categoria, il suo team, il
suo modulo di apertura e le sue regole.

---

## Il flusso

1. Crei uno o più **pannelli**.
2. VionDefence pubblica un **messaggio pannello** con un selettore che li elenca.
3. Un membro ne sceglie uno. Se ha un modulo, lo compila in un popup.
4. Compare un canale privato nella categoria di quel pannello, visibile al membro e ai
   team del pannello.
5. Il support lo prende in carico, lo gestisce, lo chiude. Viene archiviato un transcript.

---

## Impostazioni del pannello

| Impostazione | Significato |
|---|---|
| **Nome** | Mostrato nel selettore, e usato da `/ticket move` |
| **Descrizione** | Sottotitolo nel selettore |
| **Emoji** | Icona nel selettore |
| **Posizione** | Ordine di visualizzazione |
| **Attivo** | Nasconde il pannello senza eliminarlo |
| **Categoria** | Dove vengono creati i canali dei ticket |
| **Canale di log** | Dove finiscono eventi e transcript di questo pannello |
| **Template del nome ticket** | Schema del nome dei canali |
| **Team utente** | Chi può aprire un ticket qui |
| **Team support** | Chi li gestisce |
| **Team admin** | Staff elevato per questo pannello |
| **Consenti chiusura all'utente** | Se chi apre può chiudere il proprio ticket |
| **Transcript obbligatorio (support)** | Forza il transcript quando chiude il support |
| **Transcript obbligatorio (admin)** | Forza il transcript quando chiude un admin |
| **Campi del modulo** | Le domande poste all'apertura |

### Template del nome ticket

Default `ticket-{id}`. Segnaposto: `{id}` (il numero progressivo del pannello),
`{username}`, `{displayname}`.

Il risultato viene messo in minuscolo, gli spazi diventano trattini, e viene tagliato a
100 caratteri — le regole di Discord per i nomi dei canali.

---

## I team — la parte da fare bene

Ogni team è un insieme di ruoli e/o utenti.

| Team | Può |
|---|---|
| **Team utente** | Aprire un ticket su questo pannello |
| **Team support** | Vedere, prendere in carico, rilasciare e chiudere i ticket; aggiungere e rimuovere membri |
| **Team admin** | Tutto quanto sopra, più rilasciare un ticket preso in carico da un altro |

**Il team utente si comporta in modo diverso dagli altri due.** Lascialo **vuoto** e
*tutti* possono aprire ticket su quel pannello — vuoto significa nessuna restrizione.
Riempilo per rendere un pannello riservato allo staff, o limitato a un ruolo di abbonati.

I team support e admin **non** funzionano così. Un team support vuoto significa che
**nessuno** può prendere in carico o chiudere i ticket di quel pannello, e ti ritroverai
in silenzio con una pila di ticket senza risposta. Impostane sempre almeno uno.

---

## Presa in carico

Un membro del support prende in carico un ticket per segnalare che se ne sta occupando.
Mentre è preso in carico, gli altri membri del support perdono l'accesso in scrittura a
quel canale — così la conversazione resta tra chi ha aperto e un solo gestore, invece di
diventare una folla.

- **Claim** — il pulsante, o `/ticket claim`. Rifiutato se qualcun altro lo tiene già.
- **Release** — il pulsante, o `/ticket release`. Solo chi l'ha preso in carico o un
  membro del **team admin** può rilasciarlo.

---

## Il modulo di apertura

Un pannello può porre domande prima di creare il ticket. Ogni campo ha un'**etichetta**,
un **tipo** (`text` o `file`), un flag **obbligatorio**, un **placeholder** opzionale, e
**lunghezza min/max** opzionale per il testo.

Le risposte vengono pubblicate nel canale del ticket all'apertura, così il support ha
subito il contesto. Un pannello senza campi apre il ticket direttamente.

Tieni i moduli corti. A tre buone domande si risponde; a otto si rinuncia.

---

## Transcript

La chiusura apre un popup che chiede un **motivo** opzionale (max 500 caratteri).

Se venga prodotto un transcript dipende dal pannello:

- **Transcript obbligatorio** per il ruolo di chi chiude → generato sempre, non si può
  rinunciare.
- **Non obbligatorio** → il popup mostra una casella **Salva transcript**, spuntata di
  default. Chi chiude può toglierla.

I due interruttori sono indipendenti, quindi puoi imporre il transcript sulle chiusure
del support e lasciare agli admin la possibilità di chiudere in silenzio, o il contrario.

Il transcript è un file **HTML** autonomo, `transcript-ticket-<numero>.html`, pubblicato
nel **canale di log** del pannello insieme all'indicazione di chi ha chiuso.

> I transcript vanno nel canale di log **del pannello**, non nella categoria di log
> **Ticket**. La categoria riceve gli eventi — aperto, preso in carico, chiuso. Imposta
> entrambi.

---

## Chi può chiudere

| Chi chiude | Consentito |
|---|---|
| Chi ha aperto | Solo se **Consenti chiusura all'utente** è attivo |
| Team support | Sì |
| Team admin | Sì |
| Chiunque altro | No |

---

## Gestire i ticket da Discord

Dentro un canale ticket: `/ticket claim`, `/ticket release`, `/ticket add`,
`/ticket remove`, `/ticket move panel:<nome>`, `/ticket close`.

`/ticket move` serve per i ticket aperti sul pannello sbagliato: li riassegna al team e
alla categoria giusti senza perdere la conversazione.

---

## Risoluzione problemi

| Sintomo | Causa |
|---|---|
| Il selettore è vuoto | Tutti i pannelli sono disattivati, o il membro non è nel team utente di nessuno |
| I canali dei ticket non vengono creati | Al bot mancano **Gestire i canali** nella categoria o **Gestire i ruoli** |
| Non arriva nessun transcript | Canale di log del pannello non impostato, eliminato, o il bot non può allegare file |
| Il support non vede i ticket nuovi | Il team support è vuoto, o i suoi ruoli sono stati eliminati |

---

Avanti: **[Automod](IT-Configurazione-Automod)**
