# Ticket

[English](../tickets.md) · **Italiano**

Un sistema di ticket costruito attorno ai **pannelli**. Ogni pannello è un tipo di
richiesta — assistenza, segnalazioni, candidature — con la propria categoria, il proprio
team, il proprio modulo di apertura e le proprie regole.

Si configura nella dashboard sotto **Ticket**.

---

## Come funziona

1. Crei uno o più **pannelli** nella dashboard.
2. VionDefence pubblica un **messaggio pannello** con un selettore che li elenca.
3. Un membro sceglie un pannello. Se il pannello ha un modulo, lo compila in una
   finestra.
4. Viene creato un canale privato nella categoria del pannello, visibile al membro e ai
   team del pannello.
5. Il support lo prende in carico, lo gestisce, lo chiude. Viene archiviato un
   transcript.

---

## Impostazioni di un pannello

| Impostazione | Significato |
|---|---|
| **Nome** | Mostrato nel selettore, e usato da `/ticket move` |
| **Descrizione** | Sottotitolo nel selettore |
| **Emoji** | Icona nel selettore |
| **Posizione** | Ordine nel selettore |
| **Attivo** | Nasconde il pannello dal selettore senza eliminarlo |
| **Categoria** | Dove vengono creati i canali dei ticket |
| **Canale di log** | Dove finiscono eventi e transcript di questo pannello |
| **Template del nome ticket** | Schema del nome per i canali dei ticket |
| **Team utente** | Chi può aprire un ticket su questo pannello |
| **Team support** | Chi gestisce i ticket di questo pannello |
| **Team admin** | Staff elevato per questo pannello |
| **Consenti chiusura all'utente** | Se chi l'ha aperto può chiuderlo |
| **Transcript obbligatorio (support)** | Forza il transcript quando chiude il support |
| **Transcript obbligatorio (admin)** | Forza il transcript quando chiude un admin |
| **Campi del modulo** | Le domande poste all'apertura |

### Template del nome ticket

Default: `ticket-{id}`.

| Segnaposto | Sostituito con |
|---|---|
| `{id}` | Il numero di ticket del pannello, progressivo per pannello |
| `{username}` | Il nome utente Discord di chi lo apre |
| `{displayname}` | Il suo nickname su questo server |

Il risultato viene messo in minuscolo, gli spazi diventano trattini, e viene tagliato a
100 caratteri — le regole di Discord per i nomi dei canali.

---

## Team

Ogni team è un insieme di **ruoli** e/o **utenti**.

| Team | Può |
|---|---|
| **Team utente** | Aprire un ticket su questo pannello |
| **Team support** | Vedere, prendere in carico, rilasciare, chiudere i ticket; aggiungere e rimuovere membri |
| **Team admin** | Tutto quello che fa il support, più rilasciare un ticket preso in carico da un altro |

**Lascia il team utente vuoto per permettere a tutti di aprire ticket** su quel
pannello — un team utente vuoto significa "nessuna restrizione". Riempilo per rendere
un pannello riservato allo staff, o limitato a un ruolo di abbonati.

I team support e admin **non** seguono la regola "vuoto = tutti": un team support vuoto
significa che nessuno può prendere in carico o chiudere i ticket di quel pannello.
Impostane sempre almeno uno.

---

## Presa in carico

Un membro del support prende in carico un ticket per segnalare che se ne sta occupando.
Mentre è preso in carico, gli altri membri del support perdono l'accesso in scrittura a
quel canale — la conversazione resta tra chi ha aperto il ticket e un solo gestore,
invece di diventare una folla.

- **Claim** — `/ticket claim` o il pulsante **Claim**. Rifiutato se qualcun altro l'ha
  già preso in carico.
- **Release** — `/ticket release` o il pulsante **Release**. Solo chi l'ha preso in
  carico o un membro del **team admin** può rilasciarlo.

---

## Il modulo di apertura

Un pannello può porre delle domande prima di creare il ticket. Ogni campo ha:

| Proprietà | Significato |
|---|---|
| **Etichetta** | La domanda |
| **Tipo** | `text` o `file` |
| **Obbligatorio** | Se può essere lasciato vuoto |
| **Placeholder** | Testo di suggerimento dentro il campo |
| **Lunghezza min / max** | Limiti di lunghezza per i campi di testo |

Le risposte vengono pubblicate nel canale del ticket all'apertura, così il support ha
subito il contesto.

I pannelli senza campi aprono il ticket direttamente.

---

## Chiusura e transcript

La chiusura apre una finestra che chiede un **motivo** opzionale (max 500 caratteri).

Se venga prodotto un transcript dipende dal pannello:

- **Transcript obbligatorio** per il ruolo di chi chiude → il transcript viene sempre
  generato, non si può rinunciare.
- **Non obbligatorio** → la finestra mostra una casella **Salva transcript**, spuntata
  di default. Chi chiude può toglierla per chiudere senza transcript.

I due interruttori sono indipendenti, quindi puoi imporre il transcript quando chiude
il support e lasciare agli admin la possibilità di chiudere in silenzio, o il contrario.

Il transcript è un file **HTML** autonomo chiamato
`transcript-ticket-<numero>.html`, pubblicato nel **canale di log** del pannello
insieme all'indicazione di chi ha chiuso il ticket. Gli eventi dei ticket finiscono
anche nella categoria di log **Ticket** — vedi [Log](log.md).

### Chi può chiudere

| Chi chiude | Consentito |
|---|---|
| Chi ha aperto il ticket | Solo se **Consenti chiusura all'utente** è attivo su quel pannello |
| Team support | Sì |
| Team admin | Sì |
| Chiunque altro | No |

---

## Gestire un ticket

Dall'interno del canale del ticket:

| Comando | Effetto |
|---|---|
| `/ticket claim` | Assegnalo a te |
| `/ticket release` | Rimettilo a disposizione |
| `/ticket add user:@membro` | Aggiungi qualcuno al ticket |
| `/ticket remove user:@membro` | Rimuovilo |
| `/ticket move panel:<nome>` | Sposta il ticket nella categoria di un altro pannello |
| `/ticket close` | Chiudilo |

`/ticket move` serve per i ticket aperti sul pannello sbagliato — li riassegna al team
giusto senza perdere la conversazione.

---

## Risoluzione problemi

**Il selettore non mostra nessun pannello.** Sono tutti disattivati, oppure il membro
non fa parte del team utente di nessun pannello.

**I canali dei ticket non vengono creati.** A VionDefence servono **Gestire i canali**
nella categoria del pannello e **Gestire i ruoli** per scrivere i permessi.

**Non arriva nessun transcript.** Il canale di log del pannello non è impostato, è stato
eliminato, oppure il bot non può inviare allegati lì dentro.

**Il support non vede i ticket nuovi.** Il team support è vuoto, o i ruoli che conteneva
sono stati eliminati.

---

Avanti: [Log](log.md)
