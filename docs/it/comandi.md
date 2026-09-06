# Riferimento dei comandi

[English](../commands.md) · **Italiano**

Ogni comando di VionDefence è un comando slash di Discord. Le risposte sono
effimere — le vede solo chi ha eseguito il comando.

I comandi sono registrati globalmente, quindi compaiono in tutti i server in cui il bot
è presente, ma ogni server decide in autonomia quali sono **attivi** e **chi può
usarli** (vedi [Permessi e restrizioni](#permessi-e-restrizioni)).

---

## Moderazione

### `/kick`

Espelle un membro dal server.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `user` | sì | Il membro da espellere |
| `reason` | no | Motivo, max 512 caratteri |

### `/ban add`

Banna un membro. Il ban può essere permanente o temporaneo.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `user` | sì | Il membro da bannare |
| `reason` | no | Motivo, max 512 caratteri |
| `duration` | no | Es. `10m`, `2h`, `3d`, `1w`. Vuoto = ban permanente |

I ban temporanei vengono rimossi automaticamente alla scadenza.

### `/ban remove`

Rimuove il ban da un membro.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `user` | sì | Il membro da sbannare |
| `reason` | no | Motivo dello sban |

### `/ban info`

Tutto quello che è registrato su un singolo ban: stato, destinatario, moderatore,
motivo, quando è stato emesso, quando scade e — se non è più attivo — quando è stato
chiuso, da chi e perché.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `ban-id` | sì | ID della sanzione (da `/ban list`, `/userinfo` o `/userhistory`) |

L'ID deve appartenere a un **ban** emesso **in questo server**; qualsiasi altra cosa
viene segnalata come non trovata.

### `/ban list`

Elenco paginato di tutti i ban **attivi** in questo server, dal più recente. Ogni riga
riporta ID della sanzione, destinatario, moderatore, data di emissione, scadenza e
motivo.

### `/mute add`

Muta un membro usando il **ruolo mute** del server (impostato nella dashboard sotto
Moderazione). Fallisce se non è configurato nessun ruolo mute.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `user` | sì | Il membro da mutare |
| `reason` | no | Motivo, max 512 caratteri |
| `duration` | no | Es. `30m`, `12h`, `2d`. Vuoto = mute a tempo indeterminato |

### `/mute remove`

Toglie il ruolo mute a un membro.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `user` | sì | Il membro da smutare |
| `reason` | no | Motivo |

### `/mute info`

Tutto quello che è registrato su un singolo mute, con lo stesso schema di `/ban info`.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `mute-id` | sì | ID della sanzione del mute |

### `/mute list`

Elenco paginato di tutti i mute **attivi** in questo server.

### `/timeout add`

Applica un **timeout nativo di Discord**. Discord li limita a 28 giorni.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `user` | sì | Il membro da mettere in timeout |
| `duration` | sì | Es. `10m`, `2h`, `3d` — massimo 28 giorni |
| `reason` | no | Motivo, max 512 caratteri |

### `/timeout remove`

Rimuove un timeout attivo.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `user` | sì | Il membro a cui togliere il timeout |
| `reason` | no | Motivo |

### `/timeout info`

Tutto quello che è registrato su un singolo timeout, con lo stesso schema di
`/ban info`.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `timeout-id` | sì | ID della sanzione del timeout |

### `/timeout list`

Elenco paginato di tutti i timeout **attivi** in questo server.

### `/warn add`

Ammonisce un membro. I warn si accumulano e possono innescare un'escalation
automatica — vedi [Moderazione](moderazione.md#escalation-dei-warn).

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `user` | sì | Il membro da ammonire |
| `reason` | sì | Motivo, max 512 caratteri |

### `/warn remove`

Rimuove un singolo warn attivo tramite il suo ID. L'ID si trova con `/warnings`,
`/userinfo` o `/userhistory`.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `warn-id` | sì | L'ID del warn da rimuovere |
| `reason` | no | Motivo della rimozione |

### `/warn clear`

Rimuove **tutti** i warn attivi di un membro in una volta.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `user` | sì | Il membro di cui azzerare i warn |
| `reason` | no | Motivo della rimozione |

### `/warn info`

Tutto quello che è registrato su un singolo warn, con lo stesso schema di `/ban info`.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `warn-id` | sì | ID della sanzione del warn (da `/warnings` o `/userinfo`) |

### `/bulkdelete`

Elimina i messaggi più recenti del canale in cui viene eseguito, eventualmente solo
quelli inviati da un membro. Richiede il piano **Basic**.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `user` | no | Elimina solo i messaggi inviati da questo membro |
| `count` | no | Quanti messaggi eliminare, da 1 a 100 |

Cosa viene eliminato dipende dalle opzioni passate:

| Opzioni indicate | Effetto |
|---|---|
| nessuna | gli ultimi **100** messaggi del canale |
| solo `count` | gli ultimi `count` messaggi del canale |
| solo `user` | gli ultimi **50** messaggi di quel membro |
| `user` e `count` | gli ultimi `count` messaggi di quel membro |

Il comando agisce sempre sul **canale in cui viene eseguito**, mai sull'intero server.
Quando filtra per membro, VionDefence risale al massimo agli ultimi 1000 messaggi di
quel canale cercando i suoi.

Discord non permette l'eliminazione in blocco dei messaggi più vecchi di
**14 giorni**: quelli restano intatti e la risposta indica quanti sono stati saltati.

A VionDefence servono **Gestire i messaggi** e **Leggere la cronologia dei messaggi**
nel canale.

---

## Sintassi delle durate

Tutte le opzioni `duration` usano lo stesso formato compatto:

| Unità | Significato |
|---|---|
| `s` | secondi |
| `m` | minuti |
| `h` | ore |
| `d` | giorni |
| `w` | settimane |

Le unità si possono combinare e vengono sommate: `1d12h` sono 36 ore, `1w2d` sono 9
giorni. Una durata non valida o pari a zero viene rifiutata con un messaggio d'errore.

---

## Stato e sanzioni attive

### `/userinfo`

Lo stato attuale di un utente in un solo embed: età dell'account, quando è entrato nel
server, i suoi ruoli, se in questo momento è **bannato**, **mutato** o **in timeout**,
quanti warn attivi ha, l'elenco delle sue sanzioni attive con i relativi ID e i totali
per tipo di sanzione.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `user` | sì | Il membro da controllare |

Usalo quando ti serve la fotografia del momento invece del registro completo:
`/userhistory` elenca tutto quello che è successo, `/userinfo` risponde a "cosa sta
succedendo adesso con questo utente". Funziona anche su utenti che hanno lasciato il
server o che sono stati bannati.

L'embed segnala anche i casi in cui Discord e il database delle sanzioni non
concordano — un utente bannato su Discord senza una sanzione registrata, un ruolo mute
rimasto addosso, o una sanzione di timeout che Discord non sta più applicando — così
puoi sistemarli invece di lasciarli andare alla deriva.

Sui server dove gira il [sistema di livelli](livelli.md) l'embed porta anche un campo
**Livello**: il livello, gli XP totali, la posizione e gli XP che mancano al livello
successivo. Dove il sistema è spento il campo non compare affatto, invece di mostrare
una scala vuota.

Il colore segue i colori per sanzione configurati in dashboard, scegliendo quello
della sanzione più grave ancora attiva sull'utente.

### `/warnings`

Elenco paginato di tutti i warn **attivi** in questo server. È la controparte a
livello di server del conteggio warn per utente mostrato da `/userinfo`.

---

## Cronologia

### `/userhistory`

Mostra la cronologia completa delle sanzioni di un membro — ogni kick, ban, mute,
timeout e warn, con ID, stato (attiva, revocata, scaduta, chiusa), motivo e moderatore.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `user` | sì | Il membro di cui vedere la cronologia |

### `/staffhistory`

Mostra le sanzioni **emesse da** un membro dello staff. Utile per controllare il
proprio team.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `moderator` | sì | Il membro dello staff da controllare |

Entrambi i comandi paginano i risultati.

---

## Canali vocali temporanei

### `/channel-templates new`

Crea un template. Chi entra nel canale hub ottiene una nuova stanza vocale nella
categoria scelta.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `discord-category` | sì | Categoria in cui creare i nuovi canali |
| `hub-channel` | sì | Canale vocale in cui entrare per far partire la creazione |
| `channel-name-format` | sì | Schema del nome, es. `Stanza {id}` o `Stanza di {username}` |
| `max-user-count` | no | Limite utenti dei canali creati. `0` = illimitato |

Segnaposto disponibili in `channel-name-format`: `{id}`, `{username}`, `{displayname}`.

### `/channel-templates list`

Elenca tutti i template con ID, categoria, canale hub, formato del nome e limite
utenti. Paginato.

### `/channel-templates remove`

Elimina un template.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `template-id` | sì | L'ID del template, da `/channel-templates list` |

### `/channel-templates clear`

Elimina **tutti** i template del server. Non c'è nessuna conferma.

---

## Controlli del canale vocale privato

`/voice` è il comando che il membro usa sulla stanza che possiede. Ogni sottocomando
apre una finestra o un selettore — nessuno prende opzioni dirette.

| Sottocomando | Cosa fa |
|---|---|
| `/voice rename` | Rinomina la tua stanza |
| `/voice change-limit` | Imposta il limite di membri, o `0` per azzerarlo |
| `/voice change-privacy` | Passa tra **libera**, **bloccata** e **privata** |
| `/voice trust` | Fa entrare un membro specifico quando la stanza è bloccata o privata |
| `/voice untrust` | Revoca la fiducia (**non** espelle il membro) |
| `/voice kick` | Rimuove un membro dalla tua stanza |
| `/voice ban` | Impedisce a un membro di entrare (gli toglie anche la fiducia) |
| `/voice unban` | Toglie quel divieto (**non** concede la fiducia) |
| `/voice claim` | Prende possesso della stanza, solo se il proprietario precedente l'ha lasciata |

Le stesse azioni sono disponibili come pulsanti sul pannello di controllo della stanza
— vedi [Canali vocali](canali-vocali.md).

---

## Ticket

`/ticket` funziona solo **dentro un canale ticket**.

| Sottocomando | Opzioni | Cosa fa |
|---|---|---|
| `/ticket close` | — | Chiude questo ticket |
| `/ticket claim` | — | Prende in carico questo ticket |
| `/ticket release` | — | Rilascia un ticket che avevi preso in carico |
| `/ticket add` | `user` | Aggiunge un membro al ticket |
| `/ticket remove` | `user` | Rimuove un membro dal ticket |
| `/ticket move` | `panel` | Sposta il ticket nella categoria di un altro pannello |

Vedi [Ticket](ticket.md) per come funzionano pannelli, team e transcript.

---

## Livelli e promozione

### `/level`

La scheda livello di un membro: il livello sull'ultimo, gli XP totali, la posizione sul
server e una barra di avanzamento verso il livello successivo con gli XP che mancano.
Il piè di pagina conta i messaggi e i minuti in vocale che ce l'hanno portato.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| `user` | no | Il membro da consultare. Se manca risponde su chi ha eseguito il comando |

Sui server dove il sistema di livelli è spento risponde che è disattivato, e rifiuta i
bot, che non guadagnano mai XP. Vedi [Sistema di livelli](livelli.md).

### `/bump`

Mette questo server nella **descrizione Discord del bot** — nome e link di invito — per
una finestra estratta a caso tra 12 e 24 ore.

Non ha opzioni: cosa viene scritto si imposta una volta dalla dashboard.

Su tutto il bot può occupare lo slot **un server per volta**. Mentre è occupato il
comando risponde dicendo quando si libera. Eseguirlo può anche pagare XP, se la
dashboard imposta un premio e il sistema di livelli è attivo.

Richiede il piano **Basic**. Vedi [Bump ME](bump.md).

---

## Utilità

### `/ping`

Restituisce la tua latenza con il bot in millisecondi.

**Disattivo di default** — attivalo nella dashboard sotto **Comandi** se lo vuoi.

---

## Permessi e restrizioni

Ogni comando ha quattro impostazioni indipendenti nella sezione **Comandi** della
dashboard:

| Impostazione | Effetto |
|---|---|
| **Attivo** | Disattiva del tutto il comando su questo server |
| **Permesso** | Il permesso Discord che il membro deve avere per usarlo |
| **Ruoli** | Se non è vuota, solo questi ruoli possono usarlo |
| **Canali** | Se non è vuota, il comando funziona solo in questi canali |

Ruoli e canali sono **liste di permessi**: lasciarle vuote significa "nessuna
restrizione". I controlli si sommano con AND — se imposti sia un permesso sia una lista
di ruoli, al membro servono il permesso **e** uno dei ruoli. Impostare il permesso su
*nessuno* disattiva il controllo sui permessi.

### Valori predefiniti

| Comando | Attivo | Permesso richiesto |
|---|---|---|
| `/kick` | sì | Espellere membri |
| `/ban` | sì | Bannare membri |
| `/warn` | sì | Moderare membri |
| `/mute` | sì | Moderare membri |
| `/timeout` | sì | Moderare membri |
| `/userinfo` | sì | Moderare membri |
| `/warnings` | sì | Moderare membri |
| `/userhistory` | sì | Moderare membri |
| `/staffhistory` | sì | Moderare membri |
| `/bulkdelete` | sì | Gestire i messaggi |
| `/channel-templates` | sì | Gestire i canali |
| `/voice` | sì | nessuno — tutti |
| `/level` | sì | nessuno — tutti |
| `/bump` | sì | nessuno — tutti |
| `/ticket` | sì | nessuno — tutti |
| `/ping` | **no** | nessuno — tutti |

### Regole di sicurezza sempre attive

Qualunque sia la configurazione, VionDefence si rifiuta di:

- far sanzionare un moderatore da **sé stesso**;
- far sanzionare **il bot** da chiunque;
- agire su un membro che sta **sopra il bot** nella gerarchia dei ruoli — Discord
  rifiuterebbe comunque l'azione.

---

Avanti: [Moderazione](moderazione.md)
