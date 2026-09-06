# Configurazione — Livelli

[English](Configuration-Levels) · **Italiano**

*Dashboard → il tuo server → **Livelli***

I membri guadagnano XP partecipando, gli XP comprano livelli, i livelli assegnano
premi. Una volta impostato va da solo: non esiste un comando per dare XP a mano.

Incluso dal piano **Free**. Di default è **spento**.

---

## Impostalo in cinque minuti

1. Attiva **il sistema di livelli**.
2. Lascia la curva com'è (base 100, moltiplicatore `1 + ({level} - 1) * 0.5`, ultimo
   livello 100). È una scala sensata e la puoi correggere dopo senza perdere niente.
3. Per ora lascia le whitelist **vuote**: conta ogni canale.
4. Scegli un **canale per la notifica** — uno che i membri leggano davvero.
5. Salva e manda un messaggio per verificare che gli XP inizino a muoversi.

I premi aggiungili dopo, quando vedi con che velocità la gente sta salendo davvero.

---

## Come si guadagna XP

| Impostazione | Default | Significato |
|---|---|---|
| **XP per messaggio** | 5 | Guadagnati da un messaggio in un canale conteggiato |
| **Attesa** | 60 s | Un membro guadagna da un messaggio al massimo una volta per finestra |
| **XP al minuto in vocale** | 2 | Guadagnati per ogni minuto intero in un vocale conteggiato |

Metti un valore a **0** per spegnere quella fonte senza spegnere tutto il sistema.

Non mettere l'attesa a 0. Senza attesa la scala misura la velocità di battitura invece
della partecipazione, e il modo più rapido per salire diventa riempire un canale vuoto.

### La sessione in vocale

Il tempo in vocale va dall'entrata all'uscita, contato in minuti interi. Passare da un
canale vocale a un altro dello stesso server **continua la stessa sessione**: i tratti
vengono sommati e scritti insieme, quindi la notifica di livello scatta una volta sola,
quando il membro esce davvero dal vocale — non a ogni salto.

---

## Dove si guadagna XP

Tre elenchi — categorie, canali testuali, canali vocali — più i ruoli che non guadagnano
mai.

| Whitelist | Cosa conta |
|---|---|
| Tutte vuote | Ogni canale del server |
| Anche una voce sola | Solo i canali elencati e tutto quello che sta nelle categorie elencate |

Elencare una **categoria** copre quello che contiene in quel momento, quindi i canali
spostati dentro dopo iniziano a contare da soli. Di solito è quello che vuoi: elenca le
categorie, non i singoli canali.

Escludi i canali AFK, quelli dei comandi bot e quelli della musica. Dare XP per stare in
AFK tutta la notte rende la scala priva di senso.

---

## La curva dei livelli

| Impostazione | Default | Significato |
|---|---|---|
| **XP minima per ogni livello** | 100 | Il costo di base. Un livello non costa mai meno |
| **Moltiplicatore XP** | `1 + ({level} - 1) * 0.5` | Una formula per cui si moltiplica la base |
| **Ultimo livello** | 100 | La cima della scala |

Il costo di un livello è `XP minima × moltiplicatore`, arrotondato. Il pannello stampa i
primi dieci livelli mentre scrivi: guarda quella tabella invece di fidarti della formula.

### La formula

Placeholder: `{level}`, `{base_xp}`, `{max_level}` e `{previous}` (quanto è costato il
livello precedente). Operatori `+ - * / % ^`, parentesi e `min`, `max`, `pow`, `floor`,
`ceil`, `round`, `abs`, `sqrt`, `log`. Tutto il resto viene rifiutato al salvataggio, con
la spiegazione: è un'espressione matematica, non codice.

| Se vuoi | Scrivi |
|---|---|
| Ogni livello costa uguale | `1` |
| Una salita morbida | `1 + ({level} - 1) * 0.5` |
| Ogni livello costa il suo numero di basi | `{level}` |
| Una salita ripida | `{level} ^ 1.5` |
| Ripida all'inizio, piatta dal livello 20 | `min({level}, 20)` |

### Cambiarla dopo

I livelli si calcolano sugli XP che ogni membro ha già, quindi una curva nuova sposta
tutti insieme. Nessuno perde XP, ma una curva più cara può far scendere un membro dal
livello 12 al 7. I premi già assegnati non vengono tolti.

Decidi la curva prima di annunciare il sistema. I membri notano molto di più un livello
che va indietro che uno che arriva in ritardo.

---

## Premi

Ogni livello ne accetta fino a due: un **ruolo** e una **gratifica testuale**.

- **Ruolo** — assegnato al raggiungimento del livello, mai tolto. Il bot ha bisogno di
  *Gestisci Ruoli* e deve stare **sopra** al ruolo; la dashboard rifiuta i ruoli che non
  riuscirebbe ad assegnare, quindi un rifiuto qui vuol dire che il bot è troppo in basso
  nell'elenco dei ruoli.
- **Gratifica testuale** — una riga aggiunta alla notifica di livello.

Attraversare più livelli in una volta — dopo una lunga sessione in vocale — assegna i
premi di **tutti** i livelli attraversati, con una notifica sola.

Limiti per piano: 10 premi su Free, 25 su Basic, 50 su Pro, 100 su Ultimate.

Placeholder per la notifica e per le gratifiche: `{user}`, `{username}`,
`{displayname}`, `{level}`, `{previous_level}`, `{xp}`, `{guild}`.

---

## La notifica

Scegli un canale testuale, oppure lascialo vuoto per mandare la notifica in **messaggio
privato**. Se il canale scelto sparisce, la notifica ripiega sul privato invece di
perdersi.

A parte questo, la categoria di log **Livelli** ([Log](IT-Configurazione-Log)) registra
per lo staff ogni passaggio di livello, compresi i ruoli premio che non è stato possibile
assegnare. Puntala su un canale dello staff: è lì che scoprirai che il bot sta sotto a un
ruolo premio.

---

## Cosa vedono i membri

`/level [utente]` mostra livello, XP, posizione e avanzamento verso il livello
successivo. `/userinfo` riporta gli stessi numeri in un campo **Livello**.

La dashboard mostra la **classifica** completa, con messaggi e minuti in vocale per ogni
membro.

---

## Problemi comuni

**Nessuno guadagna XP.** Il sistema è spento, oppure tutti i canali che contano stanno
fuori dalle whitelist. Ricorda che una whitelist vuota conta tutto, una riempita a metà no.

**Il ruolo premio non viene assegnato.** Il bot sta sotto a quel ruolo nell'elenco, o ha
perso *Gestisci Ruoli*. Controlla la categoria di log **Livelli**: l'errore è scritto lì
con il nome del ruolo.

**I livelli sono scesi dopo che ho cambiato la curva.** È previsto: i livelli si
ricalcolano sugli XP esistenti. Rimetti i numeri di prima e tornano.

**Gli XP del vocale non arrivano.** Vengono scritti quando il membro **esce** dal vocale,
non mentre ci sta dentro. Controlla dopo che si è disconnesso.

---

Avanti: [Bump ME](IT-Configurazione-Bump) · [Log](IT-Configurazione-Log)
