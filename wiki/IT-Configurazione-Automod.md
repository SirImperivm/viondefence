# Configurazione — Automod

[English](Configuration-Automod) · **Italiano**

*Dashboard → il tuo server → **Automod***

Tre filtri indipendenti, tutti **spenti** di default. Leggi la sezione sull'attivazione
prima di accenderne uno con un'azione collegata.

---

## Modalità di azione

Ogni modulo ha lo stesso interruttore:

| Modalità | A una violazione |
|---|---|
| **Passiva** | Il messaggio viene gestito e la violazione registrata. Nessuna sanzione. |
| **Passiva + attiva** | Lo stesso, più una sanzione che scegli tu. |

In **passiva + attiva** scegli l'azione — `warn`, `kick`, `ban`, `mute` o `timeout` — una
**durata** dove serve, e un **motivo** opzionale registrato sulla sanzione e mostrato al
membro.

Le sanzioni dell'automod passano dalla normale pipeline di moderazione: compaiono in
`/userhistory`, rispettano il ruolo mute, usano i
[colori degli embed](IT-Configurazione-Moderazione#colori-degli-embed) della sanzione, e
scadono regolarmente. Come moderatore emittente risulta il bot.

Un'azione `timeout` **senza durata non fa niente**. Impostane una.

---

## Esenzioni

Tre impostazioni che valgono per tutti e tre i moduli insieme:

| Impostazione | Effetto |
|---|---|
| **Ruoli esenti** | Chi ha uno di questi ruoli non viene mai controllato |
| **Utenti esenti** | Questi membri specifici non vengono mai controllati |
| **Rispetta la gerarchia dei ruoli** | Se attiva, i membri sopra il bot non vengono mai controllati |

Lascia *Rispetta la gerarchia dei ruoli* attiva se non hai un motivo preciso: evita che
il bot tenti ripetutamente azioni che Discord rifiuterebbe comunque.

I messaggi dei bot e quelli di sistema vengono sempre ignorati.

Metti subito i ruoli del tuo staff tra i **ruoli esenti**. I moderatori che postano link
in un canale staff sono di gran lunga il falso positivo più comune.

---

## Anti-flood

Spam di messaggi e ripetizione copia-incolla.

| Impostazione | Default | Significato |
|---|---|---|
| **Messaggi massimi** | 5 | Quanti messaggi nella finestra lo fanno scattare |
| **Intervallo** | 7 s | La finestra scorrevole |
| **Messaggi duplicati massimi** | 3 | Quanti messaggi identici di fila lo fanno scattare |

Le due condizioni sono controllate separatamente: 5 messaggi diversi in 7 secondi è
flood, e lo è anche lo stesso messaggio tre volte. Il conteggio è per membro per server,
e si azzera man mano che la finestra scorre.

Se hai una chat generale movimentata, alza **messaggi massimi** prima di allungare
l'intervallo: una conversazione vivace assomiglia al flood a 5/7s.

---

## Anti-pubblicità

| Impostazione | Default | Significato |
|---|---|---|
| **Blocca inviti Discord** | on | Blocca `discord.gg/…` e `discord.com/invite/…` |
| **Blocca link** | on | Blocca qualsiasi URL `http://` o `https://` |
| **Domini in whitelist** | vuota | Sempre consentiti |

I due blocchi sono indipendenti. La configurazione più comune è **inviti bloccati, link
liberi**: non vuoi che si pubblicizzino altri server, ma vuoi che la gente condivida un
video YouTube.

Se tieni **blocca link** attivo, metti `youtube.com`, `github.com`, `tenor.com` e
qualsiasi altra cosa usi la tua community nella whitelist. La whitelist agisce solo su
*blocca link*, non sul blocco degli inviti.

---

## Anti-insulti

Il modulo basato su AI. Legge il messaggio, decide se è un insulto e ne valuta la
gravità.

| Impostazione | Default | Significato |
|---|---|---|
| **Sensibilità** | media | Quanto è severo |
| **Messaggi di contesto** | 5 | Quanti messaggi precedenti vengono passati come contesto |

| Sensibilità | Intercetta |
|---|---|
| **Bassa** | Solo insulti gravi |
| **Media** | Moderati e gravi |
| **Alta** | Tutto, compresi quelli lievi |

I **messaggi di contesto** sono ciò che permette al classificatore di distinguere una
battuta tra amici da un attacco vero. Più contesto è più preciso e un po' più lento. `5`
è un buon default; `0` giudica ogni messaggio da solo e fraintende le prese in giro.

Le violazioni finiscono nella categoria di log **Automod AI**, separata dagli altri due
moduli — instradala dove il tuo staff la leggerà davvero. Vedi
[Log](IT-Configurazione-Log).

---

## Come attivarli

Accendere `ban` su un filtro non tarato è il modo per perdere membri per un falso
positivo. Fai invece così:

1. Attiva un modulo in **passiva**.
2. Punta **Automod** e **Automod AI** su un canale riservato allo staff.
3. Osserva per qualche giorno. Aggiungi ai ruoli esenti lo staff e i bot di cui ti fidi.
4. Taratura di soglie e whitelist finché il log non è fatto quasi solo di veri positivi.
5. Solo a quel punto passa a **passiva + attiva**, partendo da `warn`.
6. Alza l'azione più avanti, quando il log si sarà guadagnato la tua fiducia.

Un modulo alla volta. Tre filtri non tarati che scattano insieme sono impossibili da
attribuire.

---

Avanti: **[Log](IT-Configurazione-Log)** · torna alla **[Home](IT-Home)**
