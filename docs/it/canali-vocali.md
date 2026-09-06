# Canali vocali temporanei

[English](../voice-channels.md) · **Italiano**

VionDefence ha due sistemi distinti per le stanze vocali su richiesta. Da fuori si
somigliano, ma fanno lavori diversi.

| | Canali template | Canali privati |
|---|---|---|
| Scopo | Stanze generiche di sfogo | Una stanza personale per membro |
| Proprietario | Nessuno | Il membro che l'ha creata |
| Le impostazioni sopravvivono | No | Sì — ricordate per la volta dopo |
| Controlli per il membro | Nessuno | Completi: nome, limite, privacy, trust, kick, ban |
| Numero di hub | Molti template | Un sistema per server |

Usa i **canali template** per stanze in stile "Gaming 1, Gaming 2, Gaming 3…".
Usa i **canali privati** quando ogni membro deve avere una stanza che possiede davvero.

Puoi tenerli attivi entrambi — usano canali hub diversi.

---

## Canali template

Si configurano nella dashboard sotto **Canali template**, oppure con
[`/channel-templates`](comandi.md#canali-vocali-temporanei).

### Come funziona

1. Un membro entra nel **canale hub** del template.
2. VionDefence crea un nuovo canale vocale nella **categoria** del template, con il
   nome ricavato dal **formato del nome** e il **limite utenti** del template.
3. Il membro viene spostato dentro.
4. Quando esce l'ultima persona, il canale viene eliminato.

### Impostazioni

| Impostazione | Significato |
|---|---|
| **Categoria** | Dove vengono creati i nuovi canali |
| **Canale hub** | Il canale vocale in cui entrare per far partire la creazione |
| **Formato del nome** | Lo schema del nome per i nuovi canali |
| **Limite utenti** | Limite sui canali creati. `0` = illimitato |

### Segnaposto del formato del nome

| Segnaposto | Sostituito con |
|---|---|
| `{id}` | Un numero progressivo, unico per template |
| `{username}` | Il nome utente Discord di chi ha avviato la creazione |
| `{displayname}` | Il suo nickname su questo server, o il nome utente se non ne ha |

Esempi: `Stanza {id}` → `Stanza 1`, `Stanza 2`… · `Stanza di {displayname}` →
`Stanza di Marco`.

Puoi creare tutti i template che il tuo piano consente, ognuno con il proprio hub.

> Un canale hub può appartenere a un solo template. Provare a riusarne uno viene
> rifiutato.

---

## Canali privati

Si configurano nella dashboard sotto **Canali privati**.

### Impostazioni

| Impostazione | Significato |
|---|---|
| **Attivo** | Accende o spegne l'intero sistema |
| **Canale hub** | Il canale vocale in cui entrare per ottenere la propria stanza |
| **Categoria** | Dove vengono create le stanze personali |

Sia il canale hub sia la categoria sono **obbligatori** per attivare il sistema.

### Come funziona

Un membro entra nell'hub e ottiene la propria stanza, creata nella categoria. Ne è il
**proprietario**, e VionDefence ricorda le sue impostazioni — nome, limite utenti,
privacy, lista dei fidati, lista dei bannati — così la stanza successiva che apre torna
com'era.

Il nome predefinito della stanza è `House of {username}`; sono disponibili sia
`{username}` sia `{displayname}` come segnaposto.

La stanza viene eliminata quando si svuota, ma le impostazioni del proprietario restano.

### Modalità di privacy

| Modalità | Chi la vede | Chi può entrare |
|---|---|---|
| **Libera** | Tutti | Tutti |
| **Bloccata** | Tutti | Solo il proprietario e i membri fidati |
| **Privata** | Solo il proprietario e i membri fidati | Solo il proprietario e i membri fidati |

**Bloccata** è la via di mezzo utile: si vede che la stanza esiste e chi c'è dentro, ma
non ci si può entrare.

### Controlli del proprietario

Il proprietario gestisce la stanza con il comando
[`/voice`](comandi.md#controlli-del-canale-vocale-privato) oppure con il pannello di
pulsanti che VionDefence pubblica per la stanza.

| Controllo | Effetto |
|---|---|
| **Rinomina** | Cambia il nome della stanza |
| **Cambia limite** | Imposta il tetto di membri, `0` per toglierlo |
| **Cambia privacy** | Passa tra libera / bloccata / privata |
| **Trust** | Fa entrare un membro specifico quando è bloccata o privata |
| **Untrust** | Revoca la fiducia. **Non** lo rimuove se è già dentro |
| **Kick** | Rimuove subito un membro dalla stanza |
| **Ban** | Impedisce a un membro di entrare. Gli revoca anche la fiducia |
| **Unban** | Toglie il divieto. **Non** concede la fiducia |
| **Claim** | Prende possesso, solo se il proprietario precedente ha lasciato la stanza |

Le liste dei fidati e dei bannati sono salvate per proprietario e riutilizzate nelle
sessioni successive.

**Claim** esiste per il caso in cui il proprietario si disconnetta lasciando dentro
altre persone in una stanza orfana — uno di loro ne prende il controllo invece di
ritrovarsi in una stanza ingestibile. Viene rifiutato finché il proprietario è ancora
dentro.

---

## Risoluzione problemi

**Le stanze non vengono create.** Verifica che VionDefence abbia **Gestire i canali**
nella categoria di destinazione e **Spostare membri** sul server. Guarda le categorie
di log **Canali template** / **Canali privati** per l'errore reale.

**Le stanze vengono create ma il membro resta nell'hub.** Al bot manca **Spostare
membri**.

**Le stanze non vengono eliminate quando si svuotano.** Il bot ha perso **Gestire i
canali** sulla categoria dopo la creazione, oppure il canale è stato spostato fuori
manualmente.

**I cambi di privacy non hanno effetto.** Il ruolo VionDefence deve poter modificare
i permessi della stanza — gli servono **Gestire i ruoli** e **Gestire i canali**.

---

Avanti: [Ticket](ticket.md)
