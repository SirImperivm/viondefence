# Sistema di livelli

[English](../levels.md) · **Italiano**

I membri guadagnano XP scrivendo in chat e passando tempo nei canali vocali. Gli XP
comprano livelli, i livelli assegnano premi. Una volta configurato funziona da solo:
non esiste un comando per dare o togliere XP a mano.

Disponibile dal piano **Free**.

---

## Come si guadagna XP

Le fonti sono tre e ognuna si spegne da sola mettendo il suo valore a zero.

| Fonte | Quanto | Quando viene scritto |
|---|---|---|
| Messaggi testuali | `XP per messaggio`, una volta per finestra di attesa | Subito |
| Tempo in vocale | `XP al minuto` × minuti interi di collegamento | All'uscita dal vocale |
| `/bump` | Gli XP impostati nel pannello [Bump ME](bump.md) | Subito |

### Testo

Ogni messaggio inviato in un canale conteggiato guadagna gli XP configurati, ma solo
una volta per **attesa** (60 secondi di default). Senza attesa basterebbe riempire un
canale per salire in pochi secondi; con l'attesa la scala misura la presenza e non la
velocita' di battitura.

I messaggi cancellati dall'automod o dal filtro contenuti guadagnano comunque XP: i
due sistemi lavorano indipendentemente.

### Vocale

Il tempo in vocale si misura dall'entrata in un canale conteggiato fino all'uscita.
Contano solo i **minuti interi**: 90 secondi valgono un minuto di XP.

Passare da un canale vocale a un altro **dello stesso server** non chiude la sessione:
gli XP di ogni tratto vengono sommati e scritti insieme. Per questo la notifica di
passaggio di livello arriva solo quando il membro esce del tutto dal vocale, e chi
salta fra cinque canali riceve una notifica invece di cinque.

Se il bot si riavvia mentre un membro e' collegato, il tempo maturato fino a quel
momento viene scritto prima dello spegnimento e il conteggio riparte dall'avvio.

---

## Dove si guadagna XP

Il pannello **Dove si guadagna XP** contiene tre elenchi — categorie, canali testuali
e canali vocali — piu' l'elenco dei ruoli che non guadagnano mai nulla.

La regola e':

- **Tutti e tre gli elenchi vuoti** → conta ogni canale del server.
- **Anche una sola voce aggiunta** → contano solo i canali elencati e tutti i canali
  contenuti nelle categorie elencate.

Una categoria copre quello che contiene in quel momento, quindi un canale spostato
dentro una categoria conteggiata inizia a contare senza toccare nulla qui.

I bot non guadagnano mai XP, qualunque cosa dicano gli elenchi.

---

## La curva dei livelli

Tre impostazioni decidono quanto e' ripida la scala.

| Impostazione | Cosa fa |
|---|---|
| **XP minima per ogni livello** | Il costo di base. Un livello non costa mai meno di questo. |
| **Moltiplicatore XP** | Una formula: il costo di base viene moltiplicato per quello che produce. |
| **Ultimo livello** | La cima della scala. Gli XP guadagnati oltre non vengono conservati. |

Il costo del livello *N* e' `XP minima × moltiplicatore(N)`, arrotondato e mai sotto
l'XP minima. La dashboard mostra i primi dieci livelli mentre scrivi, cosi' la forma
della curva si vede prima di salvarla.

### Scrivere il moltiplicatore

Il moltiplicatore e' un'espressione aritmetica. Puo' usare:

| Placeholder | Valore |
|---|---|
| `{level}` | Il livello che si sta calcolando, si parte da 1 |
| `{base_xp}` | L'XP minima per ogni livello |
| `{max_level}` | L'ultimo livello |
| `{previous}` | Quanto e' costato il livello precedente |

Gli operatori `+ - * / % ^`, le parentesi e le funzioni `min`, `max`, `pow`, `floor`,
`ceil`, `round`, `abs`, `sqrt` e `log`. Nient'altro viene accettato: una formula che
usa qualcosa fuori da questo elenco viene rifiutata al salvataggio, con la spiegazione.

### Esempi

| Formula | Andamento | Costo livello 1 / 5 / 10, base 100 |
|---|---|---|
| `1` | Piatto, ogni livello costa uguale | 100 / 100 / 100 |
| `1 + ({level} - 1) * 0.5` | Morbido, e' quello predefinito | 100 / 300 / 550 |
| `{level}` | Lineare | 100 / 500 / 1000 |
| `{level} ^ 1.5` | Ripido | 100 / 1118 / 3162 |
| `min({level}, 20)` | Sale e poi si appiattisce al livello 20 | 100 / 500 / 1000 |

Una formula il cui costo supera quello che si puo' contare, o finisce a zero o sotto,
viene rifiutata invece che salvata: lascerebbe i membri fermi a un livello che non
possono mai superare.

### Cambiare la curva dopo

La curva si calcola sugli XP che ogni membro ha gia', quindi cambiarla sposta tutti
insieme: nessuno perde XP, ma chi era al livello 12 con una curva economica puo'
ritrovarsi al livello 7 con una piu' cara. I premi gia' assegnati non vengono tolti.

Abbassare l'**ultimo livello** elimina i premi appesi sopra la nuova cima, visto che
non potrebbero piu' scattare.

---

## Premi

Ogni livello puo' avere fino a due premi: un **ruolo** e una **gratifica testuale**.

- **Ruolo** — assegnato nel momento in cui si raggiunge il livello e mai tolto. Il bot
  ha bisogno di *Gestisci Ruoli* e deve stare **sopra** a quel ruolo nell'elenco; la
  dashboard rifiuta un ruolo che non riuscirebbe ad assegnare.
- **Gratifica testuale** — una riga di testo aggiunta alla notifica di livello.

Chi attraversa piu' livelli in una volta sola — per esempio con una lunga sessione in
vocale — riceve i premi di **tutti** i livelli attraversati, ma una notifica sola.

Quanti premi si possono impostare dipende dal piano: 10 su Free, 25 su Basic, 50 su
Pro, 100 su Ultimate. Scendere di piano taglia l'elenco a partire dai livelli piu' alti.

### Placeholder

Sia la notifica di livello sia le gratifiche testuali accettano:

| Placeholder | Sostituito con |
|---|---|
| `{user}` | La menzione del membro |
| `{username}` | Il suo nome utente Discord |
| `{displayname}` | Il suo soprannome su questo server |
| `{level}` | Il livello appena raggiunto |
| `{previous_level}` | Il livello da cui arrivava |
| `{xp}` | I suoi XP totali |
| `{guild}` | Il nome del server |

---

## La notifica di livello

Imposta un canale testuale, oppure lascia il canale vuoto per mandarla in **messaggio
privato**. Se il canale scelto viene cancellato o non e' un canale testuale, la
notifica ripiega sul messaggio privato invece di perdersi.

Chi ha i messaggi privati chiusi semplicemente non la riceve; il livello e i premi
vengono applicati lo stesso.

A parte la notifica, la categoria di log **Livelli** registra per lo staff ogni
passaggio di livello — vedi [Log](log.md).

---

## Comandi

`/level [utente]` mostra il livello, gli XP totali, la posizione sul server e gli XP
che mancano al livello successivo. Senza l'opzione `utente` risponde su chi ha
eseguito il comando.

`/userinfo` riporta gli stessi numeri in un campo **Livello**, accanto al quadro di
moderazione — ma solo sui server dove il sistema di livelli e' attivo.

Vedi [Comandi](comandi.md) per il riferimento completo.

---

## Classifica

La dashboard elenca tutti i membri che hanno guadagnato XP, ordinati per XP totali,
con livello, numero di messaggi e minuti in vocale. E' in sola lettura: la scala si
costruisce solo su quello che i membri hanno fatto davvero.

---

Avanti: [Bump ME](bump.md)
