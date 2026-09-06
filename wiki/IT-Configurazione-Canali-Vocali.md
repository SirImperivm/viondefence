# Configurazione — Canali vocali

[English](Configuration-Voice-Channels) · **Italiano**

*Dashboard → il tuo server → **Canali template** e **Canali privati***

Due sistemi distinti. Da fuori si somigliano e risolvono problemi diversi.

| | Canali template | Canali privati |
|---|---|---|
| Servono per | Stanze generiche di sfogo | Una stanza personale per membro |
| Proprietario | Nessuno | Il membro che l'ha aperta |
| Impostazioni ricordate | No | Sì, per membro |
| Controlli per il membro | Nessuno | Rinomina, limite, privacy, trust, kick, ban |
| Quanti hub | Molti template | Un sistema per server |

Puoi usarli entrambi — usano canali hub diversi.

---

## Canali template

*Dashboard → **Canali template***

Per stanze in stile "Gaming 1, Gaming 2, Gaming 3…" — che compaiono quando la precedente
si riempie e spariscono quando si svuotano. Non le possiede nessuno.

### Come funziona

1. Un membro entra nel **canale hub** del template.
2. Compare un nuovo canale vocale nella **categoria** del template, con il nome ricavato
   dal **formato del nome** e il **limite utenti** del template.
3. Il membro viene spostato dentro.
4. Viene eliminato nel momento in cui esce l'ultima persona.

### Creare un template

| Campo | Significato |
|---|---|
| **Categoria** | Dove vengono creati i nuovi canali |
| **Canale hub** | Il canale vocale in cui entrare per far partire la creazione |
| **Formato del nome** | Lo schema del nome |
| **Limite utenti** | Limite sui canali creati. `0` = illimitato |

Segnaposto per il formato del nome:

| Segnaposto | Diventa |
|---|---|
| `{id}` | Un numero progressivo, unico per template |
| `{username}` | Il nome utente Discord di chi ha avviato la creazione |
| `{displayname}` | Il suo nickname sul server, o il nome utente se non ne ha |

`Stanza {id}` dà *Stanza 1*, *Stanza 2*. `Stanza di {displayname}` dà *Stanza di Marco*.

Un canale hub appartiene a un solo template — riusarne uno viene rifiutato.

Puoi gestire i template anche da Discord con `/channel-templates`. Attenzione:
`/channel-templates clear` cancella tutti i template senza nessuna conferma.

---

## Canali privati

*Dashboard → **Canali privati***

Per i server dove ogni membro deve avere una stanza che controlla davvero.

### Configurazione

| Campo | Significato |
|---|---|
| **Attivo** | Accende o spegne il sistema |
| **Canale hub** | Il canale vocale in cui entrare per ottenere la propria stanza |
| **Categoria** | Dove vengono create le stanze personali |

Hub e categoria sono entrambi obbligatori prima di poterlo attivare.

### Cosa ottiene il membro

Entra nell'hub e compare la sua stanza nella categoria, con lui come **proprietario**. Le
sue impostazioni — nome, limite utenti, privacy, lista dei fidati, lista dei bannati —
vengono ricordate, quindi la stanza successiva torna com'era. La stanza viene eliminata
quando si svuota; le impostazioni restano.

Il nome predefinito è `House of {username}`; funzionano sia `{username}` sia
`{displayname}`.

### Modalità di privacy

| Modalità | Chi la vede | Chi può entrare |
|---|---|---|
| **Libera** | Tutti | Tutti |
| **Bloccata** | Tutti | Proprietario e membri fidati |
| **Privata** | Proprietario e membri fidati | Proprietario e membri fidati |

**Bloccata** è quella che vuole la maggior parte delle persone: la stanza si vede, si
vede chi c'è dentro, ma non ci si entra senza invito.

### Controlli del proprietario

Disponibili come pulsanti sul pannello della stanza, e come sottocomandi di `/voice`:

| Controllo | Effetto |
|---|---|
| Rinomina | Cambia il nome della stanza |
| Cambia limite | Imposta il tetto di membri, `0` lo toglie |
| Cambia privacy | Libera / bloccata / privata |
| Trust | Fa entrare un membro specifico quando è bloccata o privata |
| Untrust | Revoca la fiducia — **non** caccia chi è già dentro |
| Kick | Rimuove subito un membro |
| Ban | Impedisce a un membro di entrare, e gli revoca la fiducia |
| Unban | Toglie il divieto — **non** concede la fiducia |
| Claim | Prende possesso, solo se il proprietario precedente se n'è andato |

**Claim** esiste per le stanze orfane: il proprietario si disconnette, dentro ci sono
ancora altre persone, e una di loro prende il controllo invece di restare bloccata. Viene
rifiutato finché il proprietario è ancora presente.

---

## Risoluzione problemi

| Sintomo | Causa |
|---|---|
| Non viene creata nessuna stanza | Al bot manca **Gestire i canali** nella categoria |
| Le stanze compaiono ma il membro resta nell'hub | Al bot manca **Spostare membri** |
| Le stanze vuote non vengono eliminate | Il bot ha perso **Gestire i canali**, o il canale è stato spostato fuori dalla categoria a mano |
| I cambi di privacy non fanno niente | Al bot mancano **Gestire i ruoli** / **Gestire i canali** sulla stanza |

Le categorie di log **Canali template** e **Canali privati** contengono l'errore reale.
Se non le hai ancora impostate, vedi [Log](IT-Configurazione-Log).

---

Avanti: **[Ticket](IT-Configurazione-Ticket)**
