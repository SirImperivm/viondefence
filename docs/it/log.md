# Log

[English](../logs.md) · **Italiano**

VionDefence scrive un embed su Discord per ogni cosa che fa. Il logging è diviso in
**nove categorie indipendenti**, ognuna instradata sul proprio canale e con il proprio
stile.

Si configurano nella dashboard sotto **Log**.

---

## Categorie

| Categoria | Cosa ci finisce |
|---|---|
| **Generale** | Eventi a livello di server ed errori del bot che non rientrano altrove |
| **Comandi** | Uso dei comandi |
| **Moderazione** | Kick, ban, mute, timeout, warn, revoche, scadenze |
| **Canali template** | Template creati, rimossi, azzerati; canali temporanei creati ed eliminati |
| **Canali privati** | Modifiche alla configurazione del sistema, stanze create ed eliminate, passaggi di proprietà |
| **Ticket** | Ticket aperti, presi in carico, rilasciati, spostati, chiusi |
| **Automod** | Violazioni di anti-flood e anti-pubblicità |
| **Automod AI** | Solo le violazioni dell'anti-insulti |
| **Filtro contenuti** | Messaggi rimossi perché il loro contenuto non è consentito in quel canale |

**Automod AI** è tenuta apposta separata da **Automod**: i verdetti dell'AI sono quelli
che vorrai rivedere a mano, e mescolarli con le rilevazioni meccaniche di flood li
seppellisce.

---

## Impostazioni per categoria

| Impostazione | Significato |
|---|---|
| **Canale** | Dove vengono inviati gli embed di questa categoria |
| **Colore** | Il bordo sinistro dell'embed, in esadecimale |
| **URL thumbnail** | Un'immagine nell'angolo dell'embed. Opzionale |

Lasciare il **canale** vuoto disattiva la categoria — non viene inviato niente e non
fallisce niente. È il modo previsto per spegnere una categoria.

Il colore predefinito è `#777777` e non c'è thumbnail.

La categoria **Moderazione** è un caso a parte: i singoli tipi di sanzione hanno colori
propri, che per i loro eventi hanno la precedenza sul colore della categoria.
Vedi [Moderazione](moderazione.md#colori-degli-embed-di-log).

Vale la pena impostare i colori: a colpo d'occhio, rosso per Moderazione e arancione
per Automod ti dicono cos'è successo prima ancora di leggere una parola.

---

## Requisiti

La destinazione deve essere un **canale testuale** nello stesso server, e a
VionDefence servono **Vedere il canale**, **Inviare messaggi** e **Incorporare link**
lì dentro.

Se il canale viene eliminato o il bot perde l'accesso, il log viene scartato in
silenzio — l'azione che stava segnalando è comunque avvenuta.

Alcune categorie di log potrebbero non essere disponibili su tutti i piani. Una
categoria che il tuo piano non include viene saltata anche se hai configurato un canale.

---

## Un'impostazione pratica

Una categoria riservata allo staff con:

| Canale | Categorie instradate |
|---|---|
| `#log-moderazione` | Moderazione |
| `#log-automod` | Automod, Automod AI |
| `#log-ticket` | Ticket |
| `#log-canali` | Canali template, Canali privati |
| `#log-generale` | Generale, Comandi |

Separare Moderazione da Automod è la scelta che conta di più: una è il lavoro del tuo
team, l'altra è quello del filtro. Rivederle insieme rende più difficile leggere
entrambe.

I **transcript** dei ticket non seguono questo instradamento — vanno nel **canale di log
impostato su ogni pannello ticket**. Vedi [Ticket](ticket.md#chiusura-e-transcript).

---

## Timestamp

Ogni embed è marcato con data e ora. Fuso orario e formato arrivano dalle impostazioni
**Generale** del server — vedi [Primi passi](primi-passi.md#3-imposta-le-basi).

---

Avanti: [FAQ](faq.md)
