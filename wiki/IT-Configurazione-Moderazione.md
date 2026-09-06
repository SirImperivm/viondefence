# Configurazione — Moderazione

[English](Configuration-Moderation) · **Italiano**

*Dashboard → il tuo server → **Moderazione***

Cinque schede di sanzione — kick, ban, warn, mute, timeout — più il pannello di
escalation dei warn.

---

## Il ruolo mute

Si imposta sulla scheda **mute**. Finché non lo fai, ogni `/mute` e ogni azione `mute`
dell'automod fallisce.

Un ruolo mute che funziona davvero:

1. Crea un ruolo su Discord — chiamalo `Mutato`. Non dargli permessi propri.
2. Nei permessi dei canali, **nega**gli *Inviare messaggi*, *Parlare*, *Aggiungere
   reazioni* e *Inviare messaggi nei thread*.
3. In **Impostazioni server → Ruoli**, metti **VionDefence sopra il ruolo mute**. Un
   bot non può assegnare un ruolo che sta sopra il proprio.
4. Seleziona il ruolo nella dashboard.

Il passo 3 è quello che sfugge. Sembra tutto configurato e i mute continuano a fallire.

---

## Notifiche in DM

Ognuna delle cinque schede ha il suo interruttore **Avvisa l'utente in DM**. Quando è
attivo, il membro sanzionato riceve un messaggio privato con tipo, motivo e durata.

Tutti e cinque sono **attivi** di default.

Il DM è "best effort": se il membro ha chiuso i messaggi privati dai membri del server, o
ha già lasciato, la sanzione viene applicata comunque e non viene trattato come errore.

Disattivarlo per `warn` è una scelta comune sui server dove i warn si usano come note
interne più che come messaggio al membro.

---

## Colori degli embed

Ogni scheda di sanzione porta due colori, usati sugli embed del log **Moderazione** per
quel tipo di sanzione:

| Campo | Usato quando |
|---|---|
| **Colore embed (applicazione)** | La sanzione viene emessa — un ban, un warn, un mute |
| **Colore embed (revoca)** | La sanzione viene revocata da un moderatore, o scade da sola |

Il secondo campo compare solo sulle sanzioni che si possono togliere — **ban**, **warn**,
**mute** e **timeout**. Un kick non ha niente da revocare, quindi ha un colore solo.

È questo che rende un canale di log leggibile a colpo d'occhio: rosso per il ban che
parte, verde per l'unban che torna, arancione per un warn.

### Valori predefiniti

| Sanzione | Applicazione | Revoca |
|---|---|---|
| **Kick** | `#F76B15` arancione | — |
| **Ban** | `#E5484D` rosso | `#46A758` verde |
| **Warn** | `#F5A623` ambra | `#46A758` verde |
| **Mute** | `#8E4EC6` viola | `#46A758` verde |
| **Timeout** | `#3E63DD` blu | `#46A758` verde |

Cambiali con il selettore di colore, o scrivendo un valore `#RRGGBB`.

Questi colori hanno la precedenza sul colore della categoria **Moderazione** impostato
nei [Log](IT-Configurazione-Log), che resta il ripiego per gli eventi di moderazione
senza un colore proprio.

---

## Scadenza dei warn

Per quanto tempo un warn resta **attivo**.

- **Vuoto** — i warn non scadono mai da soli. Restano attivi finché un moderatore non li
  rimuove con `/warn remove` o `/warn clear`.
- **Impostato** — un warn si disattiva automaticamente una volta raggiunta quell'età.

I warn scaduti non vengono cancellati: restano in `/userhistory` con stato **scaduto**,
così la traccia sopravvive anche dopo che il warn smette di contare.

Solo i warn **attivi** contano per l'escalation.

---

## Escalation dei warn

Trasforma un numero di warn attivi in una sanzione automatica.

Ogni regola ha:

| Campo | Significato |
|---|---|
| **Soglia** | Un numero di warn attivi |
| **Azione** | `kick`, `ban`, `mute` o `timeout` |
| **Durata** | Per le azioni che ne prevedono una |
| **Motivo** | Opzionale. Se lo lasci vuoto ne viene usato uno predefinito che cita il numero di warn |

### Un esempio concreto

| Soglia | Azione | Durata |
|---|---|---|
| 3 | mute | 1h |
| 5 | timeout | 1d |
| 7 | ban | 7d |

Terzo warn attivo → mute di un'ora. Quinto → timeout di un giorno. Settimo → ban di una
settimana.

### La regola che sorprende

Le regole confrontano il numero di warn attivi in modo **esatto**, nel momento in cui il
warn viene aggiunto. Una regola a soglia 3 scatta sul terzo warn attivo e non riscatta sul
quarto.

La conseguenza: un membro fermo a 4 warn a cui ne togli uno e che poi se ne prende un
altro ripassa da 3 — e fa riscattare la regola della soglia 3. Azzerare i warn è il modo
per ripulire la fedina di qualcuno; sappi solo cosa fa riscattare.

Più regole possono condividere la stessa soglia. Scattano tutte.

Una regola `timeout` senza durata viene saltata — i timeout di Discord ne richiedono
sempre una.

---

## Controllare cosa è in vigore

I colori e le notifiche in DM di questa pagina descrivono cosa succede quando una
sanzione viene emessa. Per rileggere lo stato ci sono quattro comandi che usano la
stessa configurazione:

- `/userinfo user:@membro` — tutto lo stato di moderazione del membro in un solo embed:
  se è bannato, mutato o in timeout, quanti warn attivi ha, ogni sanzione attiva con il
  suo ID, i totali per tipo. Il colore è quello che imposti qui per la sanzione più
  grave ancora attiva su di lui.
- `/ban list`, `/mute list`, `/timeout list`, `/warnings` — tutto quello che di quel
  tipo è attivo adesso nel server, paginato.
- `/ban info`, `/mute info`, `/timeout info`, `/warn info` — una singola sanzione per
  intero, cercata tramite il suo ID.

Tutti e quattro si configurano come qualsiasi altro comando, nella sezione **Comandi**:
li attivi e decidi quali ruoli, permesso e canali possono usarli.

`/userinfo` è anche il modo più rapido per accorgersi di uno scostamento tra Discord e
il database delle sanzioni — un ban dato a mano su Discord senza sanzione dietro, un
ruolo mute rimasto addosso a un membro, o una sanzione di timeout che Discord ha già
lasciato cadere.

---

## Scadenza automatica

Ogni 30 secondi il bot toglie quello che è scaduto: i ban temporanei vengono sbannati, ai
mute viene tolto il ruolo, i warn vengono segnati come scaduti. Il membro riceve un DM, e
l'evento viene scritto nel log **Moderazione** con il colore di *revoca* della sanzione.

Se il bot è offline al momento della scadenza, la toglie al primo controllo dopo il
riavvio.

---

## Fai così adesso

1. Crea il ruolo mute, negagli i permessi giusti, e metti VionDefence sopra di esso.
2. Selezionalo sulla scheda **mute**.
3. Dai un'occhiata ai colori degli embed — i default sono sensati, cambiali se il tuo
   canale di log ha un tema.
4. Lascia scadenza ed escalation dei warn vuote finché non sai come il tuo team usa
   davvero i warn.

---

Avanti: **[Comandi](IT-Configurazione-Comandi)**
