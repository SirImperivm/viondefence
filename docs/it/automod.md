# Automod

[English](../automod.md) · **Italiano**

L'automod controlla i messaggi e reagisce alle violazioni. Ha tre moduli indipendenti,
tutti **disattivi di default**.

Si configura nella dashboard sotto **Automod**.

---

## Modalità di azione

Ogni modulo ha lo stesso interruttore a due posizioni:

| Modalità | Cosa succede a una violazione |
|---|---|
| **Passiva** | Il messaggio viene gestito e la violazione registrata. Nessuna sanzione. |
| **Passiva + attiva** | Idem, più una sanzione automatica scelta da te. |

In **passiva + attiva** scegli l'**azione attiva** — `warn`, `kick`, `ban`, `mute` o
`timeout` — e, per quelle che la prevedono, una **durata**. Puoi anche impostare un
**motivo** personalizzato, che viene registrato sulla sanzione e mostrato al membro.

Le sanzioni applicate dall'automod passano dalla normale pipeline di moderazione:
finiscono in `/userhistory`, rispettano il ruolo mute, e quelle temporanee scadono
regolarmente. Il bot stesso risulta come moderatore che le ha emesse.

> Un'azione attiva `timeout` senza durata non fa nulla. Impostane una.

---

## Esenzioni

Tre impostazioni valgono per **tutti** i moduli insieme:

| Impostazione | Effetto |
|---|---|
| **Ruoli esenti** | I membri con uno di questi ruoli non vengono mai controllati |
| **Utenti esenti** | Questi membri specifici non vengono mai controllati |
| **Rispetta la gerarchia dei ruoli** | Se attiva, i membri **sopra il bot** non vengono mai controllati |

Lascia *Rispetta la gerarchia dei ruoli* attiva se non hai un motivo per il contrario —
evita che l'automod tenti ripetutamente azioni che Discord rifiuterebbe comunque.

I messaggi dei bot e quelli di sistema vengono sempre ignorati.

---

## Anti-flood

Intercetta lo spam di messaggi e la ripetizione copia-incolla.

| Impostazione | Default | Significato |
|---|---|---|
| **Messaggi massimi** | 5 | Quanti messaggi dentro la finestra fanno scattare il filtro |
| **Intervallo** | 7 s | La finestra scorrevole in cui i messaggi vengono contati |
| **Messaggi duplicati massimi** | 3 | Quanti messaggi identici di fila fanno scattare il filtro |

Le due condizioni sono controllate separatamente: 5 messaggi diversi in 7 secondi è
flood, e lo è anche lo stesso messaggio inviato 3 volte.

Il conteggio è **per membro e per server** e si azzera quando la finestra scorre oltre.

---

## Anti-pubblicità

Intercetta inviti e link.

| Impostazione | Default | Significato |
|---|---|---|
| **Blocca inviti Discord** | on | Blocca i link `discord.gg/…` e `discord.com/invite/…` |
| **Blocca link** | on | Blocca qualsiasi URL `http://` o `https://` |
| **Domini in whitelist** | vuota | Domini sempre consentiti |

I due blocchi sono separati. Disattiva *Blocca link* e tieni *Blocca inviti Discord*
attivo se vuoi permettere il web ma non la pubblicità ad altri server.

I **domini in whitelist** agiscono solo su *Blocca link*: aggiungi `youtube.com`,
`github.com` e simili per lasciarli passare mentre tutto il resto viene intercettato.

---

## Anti-insulti

L'unico modulo basato su AI. Legge il messaggio, valuta se è un insulto e ne stima la
gravità.

| Impostazione | Default | Significato |
|---|---|---|
| **Sensibilità** | media | Quanto è severo il filtro |
| **Messaggi di contesto** | 5 | Quanti messaggi precedenti vengono passati come contesto |

### Sensibilità

| Sensibilità | Intercetta |
|---|---|
| **Bassa** | Solo gli insulti gravi |
| **Media** | Insulti moderati e gravi |
| **Alta** | Tutto, compresi quelli lievi |

Più sensibilità significa più falsi positivi. Parti da **media**, tieni il modulo in
**passiva** per qualche giorno, leggi il log, e solo dopo decidi se attivare un'azione.

### Contesto

I **messaggi di contesto** danno al classificatore i messaggi precedenti del canale,
così può distinguere una battuta tra amici da un attacco vero. Più contesto significa
più precisione e un po' più di lentezza. `5` è un default ragionevole; `0` giudica ogni
messaggio isolatamente.

Le violazioni dell'anti-insulti finiscono in una categoria di log dedicata — **Automod
AI** — separata dagli altri due moduli, così puoi mandarle su un canale diverso e
rivederle senza rumore.

---

## Attivazione consigliata

1. Attiva un modulo in modalità **passiva**.
2. Punta le categorie di log **Automod** (e **Automod AI**) su un canale riservato allo
   staff — vedi [Log](log.md).
3. Osserva per qualche giorno. Aggiungi ai ruoli esenti lo staff e i bot di cui ti fidi.
4. Aggiusta soglie e whitelist finché il log non è composto quasi solo da veri positivi.
5. Solo a quel punto passa a **passiva + attiva**, partendo da un'azione leggera come
   `warn`.

Andare dritti al `ban` su un filtro non tarato è il modo migliore per perdere membri
per un falso positivo.

---

Avanti: [Canali vocali](canali-vocali.md)
