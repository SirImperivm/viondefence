# Configurazione — Log

[English](Configuration-Logs) · **Italiano**

*Dashboard → il tuo server → **Log***

Configurali presto. I log sono il modo in cui scopri che manca un permesso, che un mute è
fallito, o che l'automod ha intercettato qualcosa che non doveva.

---

## Come funziona la sezione

C'è una scheda per ogni categoria di log. Clicca sulla **chiave inglese** di una scheda
per aprirne l'editor — un form a comparsa con tre campi:

| Campo | Cosa fa |
|---|---|
| **Canale** | Scegli la destinazione dall'elenco dei canali testuali del server. Selezionare *Disabilitato* spegne la categoria |
| **Colore embed** | La barra colorata sul lato sinistro dell'embed |
| **URL thumbnail** | Immagine opzionale nell'angolo dell'embed |

Lasciare una categoria su **Disabilitato** è il modo previsto per spegnerla: non viene
inviato niente e non fallisce niente.

---

## Le otto categorie

| Categoria | Cosa ci finisce |
|---|---|
| **Generale** | Eventi a livello di server, ed errori del bot che non rientrano altrove |
| **Comandi** | Uso dei comandi |
| **Moderazione** | Kick, ban, mute, timeout, warn, revoche, scadenze |
| **Canali template** | Template creati e rimossi; canali temporanei creati ed eliminati |
| **Canali privati** | Modifiche di configurazione, stanze create ed eliminate, passaggi di proprietà |
| **Ticket** | Ticket aperti, presi in carico, rilasciati, spostati, chiusi |
| **Automod** | Violazioni di anti-flood e anti-pubblicità |
| **Automod AI** | Solo le violazioni dell'anti-insulti |

**Automod AI** è una categoria a sé apposta. I verdetti dell'AI sono quelli che un umano
dovrebbe rivedere; mescolarli nello stesso canale delle rilevazioni meccaniche di flood
li seppellisce.

---

## Un instradamento che funziona

Crea una categoria riservata allo staff con qualche canale, invece di un unico flusso:

| Canale | Categorie |
|---|---|
| `#log-moderazione` | Moderazione |
| `#log-automod` | Automod, Automod AI |
| `#log-ticket` | Ticket |
| `#log-canali` | Canali template, Canali privati |
| `#log-generale` | Generale, Comandi |

La separazione che conta di più è **Moderazione** da **Automod**: una è il lavoro del tuo
team, l'altra quello del filtro. Leggerle mescolate rende difficili entrambe.

---

## Colori

Dai un colore a ogni categoria e riconosci un embed prima ancora di leggerlo. Rosso per
Moderazione, arancione per Automod, blu per i Ticket, grigio per Generale.

**Moderazione** va oltre: i singoli tipi di sanzione hanno i loro colori, impostati in
[Moderazione](IT-Configurazione-Moderazione#colori-degli-embed) — rosso per i ban, verde
per gli unban, arancione per i warn. Quelli hanno la precedenza sul colore della
categoria per i loro eventi. Il colore che imposti qui resta il ripiego per tutto ciò che
non ne ha uno proprio.

---

## Requisiti

La destinazione dev'essere un **canale testuale** dello stesso server, e al bot servono
**Vedere il canale**, **Inviare messaggi** e **Incorporare link**.

Se il canale viene eliminato o il bot perde l'accesso, il log viene scartato in silenzio.
L'azione che stava segnalando è comunque avvenuta — semplicemente non lo vieni a sapere.
Vale la pena ricontrollare dopo ogni revisione dei permessi.

Alcune categorie dipendono dal piano del server. Una categoria non inclusa nel tuo piano
viene saltata anche con un canale configurato.

---

## I transcript dei ticket sono un'altra cosa

I transcript **non** seguono questo instradamento: vanno nel **canale di log configurato
su ogni pannello ticket**. Vedi [Ticket](IT-Configurazione-Ticket#transcript).

---

## Fai così adesso

1. Crea un canale riservato allo staff — per iniziare basta `#log-generale`.
2. Apri **Generale** e **Moderazione** e puntali entrambi lì.
3. Dai loro due colori diversi.
4. Torna a separarli quando avrai capito che volume hanno.

---

Avanti: **[Moderazione](IT-Configurazione-Moderazione)**
