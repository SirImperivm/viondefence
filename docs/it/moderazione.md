# Moderazione

[English](../moderation.md) · **Italiano**

VionDefence registra ogni sanzione che applica, la rende consultabile, e fa scadere
da solo quelle temporanee.

Si configura nella dashboard sotto **Moderazione**.

---

## Tipi di sanzione

| Tipo | Basata su | Revocabile | Supporta una durata |
|---|---|---|---|
| **Kick** | Espulsione Discord | no | no |
| **Ban** | Ban Discord | sì | sì — oppure permanente |
| **Mute** | Il ruolo mute del server | sì | sì — oppure indeterminata |
| **Timeout** | Timeout nativo Discord | sì | sì — **obbligatoria**, max 28 giorni |
| **Warn** | Solo VionDefence | sì | scade dopo la scadenza dei warn, se impostata |

Un kick è un evento istantaneo: non c'è niente da revocare, quindi resta in cronologia
come record chiuso.

---

## Il ruolo mute

`/mute` e l'azione `mute` dell'automod hanno bisogno di un ruolo da applicare.
Impostalo sotto **Moderazione → Ruolo mute**.

Checklist per un ruolo mute che funziona davvero:

1. Crea un ruolo su Discord (es. `Mutato`) senza permessi propri.
2. Nei permessi dei canali negagli **Inviare messaggi**, **Parlare**, **Aggiungere
   reazioni** e **Inviare messaggi nei thread**.
3. Posiziona il ruolo **VionDefence** **sopra** il ruolo mute in Impostazioni server
   → Ruoli. Un bot non può assegnare un ruolo più in alto del proprio.
4. Seleziona il ruolo nella dashboard.

Senza il punto 3 i mute falliscono anche se tutto il resto sembra configurato.

---

## Notifiche in DM

Ogni tipo di sanzione ha il proprio interruttore per la **notifica in DM**. Quando è
attivo, il membro sanzionato riceve un messaggio privato con tipo, motivo e durata.

Tutti e cinque sono **attivi di default**.

Il DM è "best effort": se il membro ha disattivato i messaggi privati dai membri del
server, o ha già lasciato il server, la sanzione viene applicata comunque e il mancato
invio non è considerato un errore.

---

## Colori degli embed di log

Ogni tipo di sanzione ha i propri colori, usati sugli embed del log **Moderazione**:

| Campo | Usato quando |
|---|---|
| **Colore embed (applicazione)** | La sanzione viene emessa |
| **Colore embed (revoca)** | Viene revocata da un moderatore, o scade da sola |

Il colore di *revoca* esiste solo per le sanzioni che si possono togliere — **ban**,
**warn**, **mute** e **timeout**. Un kick non ha niente da revocare, quindi ha un colore
solo.

| Sanzione | Applicazione | Revoca |
|---|---|---|
| Kick | `#F76B15` arancione | — |
| Ban | `#E5484D` rosso | `#46A758` verde |
| Warn | `#F5A623` ambra | `#46A758` verde |
| Mute | `#8E4EC6` viola | `#46A758` verde |
| Timeout | `#3E63DD` blu | `#46A758` verde |

Hanno la precedenza sul colore della categoria **Moderazione** impostato nei
[Log](log.md#impostazioni-per-categoria), che resta il ripiego per gli eventi di
moderazione senza un colore proprio.

---

## Scadenza dei warn

La **scadenza dei warn** decide per quanto tempo un warn resta *attivo*.

- Lasciala vuota e i warn non scadono mai da soli — restano attivi finché un moderatore
  non li rimuove con `/warn remove` o `/warn clear`.
- Impostane una e ogni warn si disattiva automaticamente una volta raggiunta quell'età.

I warn scaduti non vengono cancellati. Restano visibili in `/userhistory` con stato
**scaduto**, così la traccia sopravvive anche dopo che il warn smette di contare.

Solo i warn **attivi** contano ai fini dell'escalation.

---

## Escalation dei warn

L'escalation trasforma un certo numero di warn attivi in una sanzione automatica.

Una regola ha una **soglia** (un numero di warn attivi), un'**azione** (`kick`, `ban`,
`mute` o `timeout`), una **durata** per le azioni che ne prevedono una, e un **motivo**
opzionale usato sulla sanzione automatica. Se lasci il motivo vuoto ne viene usato uno
predefinito che cita il numero di warn.

Una regola `timeout` senza durata viene saltata — i timeout di Discord richiedono
sempre una durata.

Le regole scattano su una corrispondenza **esatta** del numero di warn attivi, nel
momento in cui il warn viene aggiunto. Una regola con soglia `3` scatta quando arriva
il terzo warn attivo — non riscatta al quarto.

### Esempio

| Soglia | Azione | Durata |
|---|---|---|
| 3 | mute | 1h |
| 5 | timeout | 1d |
| 7 | ban | 7d |

Un membro che arriva a 3 warn attivi si prende un mute di un'ora. A 5, un timeout di un
giorno. A 7, un ban di una settimana.

Puoi associare più regole alla stessa soglia — scattano tutte.

> Siccome le regole confrontano il numero esatto, un membro che è a 4 warn, ne perde
> uno e poi ne prende un altro ripassa da 3 e fa riscattare la regola della soglia 3.
> Rimuovere i warn è il modo per ripulire la fedina di qualcuno; tieni presente cosa
> fa riscattare.

---

## Stato attuale

Prima di aprire la cronologia, chiediti cosa è in vigore **adesso**:

- `/userinfo user:@membro` — un solo embed con lo stato di moderazione completo del
  membro: se è bannato, mutato o in timeout, quanti warn attivi ha, ogni sanzione
  attiva con il suo ID e i totali per tipo.
- `/ban list`, `/mute list`, `/timeout list`, `/warnings` — tutto quello che di quel
  tipo è attivo adesso nel server.
- `/ban info`, `/mute info`, `/timeout info`, `/warn info` — il record completo di una
  singola sanzione a partire dal suo ID: chi l'ha emessa, quando, perché, quando
  scade e come è stata chiusa.

`/userinfo` fa emergere anche le discordanze tra Discord e il database delle sanzioni:
un utente bannato su Discord senza sanzione registrata, un ruolo mute rimasto addosso,
o una sanzione di timeout che Discord ha già lasciato cadere.

---

## Cronologia

### Su Discord

- `/userhistory user:@membro` — tutto quello che è successo a quel membro.
- `/staffhistory moderator:@staff` — tutto quello che quel membro dello staff ha emesso.

Entrambi sono paginati ed effimeri.

### Nella dashboard

La sezione **Cronologia** mostra gli stessi dati con dei filtri, e permette di aprire
una singola sanzione per vederne il dettaglio completo — moderatore, date, motivo,
revoca — e revocarla da lì.

Ogni membro ha anche una **pagina profilo**, raggiungibile dalla cronologia, che
raccoglie le sue sanzioni in un posto solo.

### Stati

| Stato | Significato |
|---|---|
| **Attiva** | In vigore adesso |
| **Revocata** | Tolta in anticipo da un moderatore |
| **Scaduta** | Finita da sola (durata esaurita, o scadenza dei warn raggiunta) |
| **Chiusa** | Non applicabile — un kick, che non ha nulla da togliere |

---

## Scadenza automatica

VionDefence controlla le sanzioni in scadenza **ogni 30 secondi** e le rimuove: i ban
temporanei vengono sbannati, ai mute viene tolto il ruolo, i warn vengono segnati come
scaduti. Il membro riceve un DM che lo avvisa della fine della sanzione, e l'evento
viene scritto nella categoria di log **Moderazione**.

Le scadenze vengono elaborate mentre il bot è in esecuzione. Se il bot è offline quando
una sanzione scade, viene rimossa al primo controllo dopo il riavvio.

---

Avanti: [Automod](automod.md)
