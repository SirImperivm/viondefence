# Configurazione — Contatori

[English](Configuration-Counters) · **Italiano**

*Dashboard → il tuo server → **Contatori***

Canali vocali che mostrano quante persone ci sono sul server. Tutti li vedono, nessuno
ci entra: sono cartelli, non stanze.

Incluso dal piano **Free**. Di default sono **spenti**.

---

## Impostalo in due minuti

1. Attiva **i contatori**.
2. Lascia l'intervallo a dieci minuti e i nomi come sono.
3. Salva. I tre canali compaiono subito, già riempiti.

Tutto il resto — la categoria, i nomi, il contatore staff — può aspettare che tu li
abbia visti al loro posto.

---

## I tre canali

| Canale | Conta | Segnaposto |
|---|---|---|
| Tutti | Ogni membro, bot compresi | `{total-count}` |
| Bot | Solo i bot | `{bots-count}` |
| Membri | Tutti tranne i bot | `{members-count}` |

Nascono con `Vedi canale` consentito e `Connetti` negato per `@everyone`. Non
aggiungerci sopra un tuo `Connetti` consentito: il canale diventerebbe accessibile e
smetterebbe di leggersi come un'etichetta.

Spegnendo i contatori i canali vengono eliminati. Non si perde nulla: i numeri arrivano
da Discord ogni volta e non sono mai salvati, quindi riaccendendoli si ricostruiscono
con i valori del momento.

---

## Il contatore staff

Un quarto canale facoltativo che conta i membri con **almeno uno** dei ruoli che
scegli. Chi ha tre ruoli staff viene comunque contato una volta sola.

La dashboard non lascia attivarlo con l'elenco dei ruoli vuoto: il contatore resterebbe
a zero per sempre e sembrerebbe rotto.

Scegli i ruoli che per i tuoi membri significano "staff", non tutti i ruoli che il tuo
staff possiede. Un ruolo `@Verificato` in quell'elenco trasforma il contatore staff in
un secondo contatore membri.

---

## I nomi

Scrivi il nome che vuoi; viene sostituito solo il segnaposto.

```
👥 Tutti: {total-count}      →      👥 Tutti: 1247
🛡 Staff: {staff-count}       →      🛡 Staff: 9
```

Ogni nome deve contenere il proprio segnaposto — un nome che non ce l'ha viene
rifiutato, perché un contatore che non cambia mai è solo un canale con un titolo
fuorviante. Discord limita i nomi a 100 caratteri e i nomi più lunghi vengono tagliati lì.

---

## L'intervallo di aggiornamento

**Discord consente due rinomine per canale ogni dieci minuti.** Superarlo non dà
errore: la richiesta viene messa in coda, e i contatori restano indietro in silenzio
proprio mentre sembrano aggiornarsi più spesso di tutti.

Per questo l'intervallo ha un minimo di **cinque minuti** e di default è dieci. Il bot
salta anche la rinomina quando il nome nuovo è uguale a quello attuale, così un server
tranquillo tiene il proprio margine per quando il numero si muove davvero.

Se ti servono conteggi immediati usa `/server stats`: ricalcola su richiesta, senza
toccare i canali.

---

## `/server stats`

Una risposta effimera, visibile solo a chi la esegue, con gli stessi numeri **più
quanti di quei membri e di quello staff sono online**.

Ricalcola invece di leggere i nomi dei canali, quindi è anche il modo più rapido per
controllare se i contatori stanno dicendo la verità.

I conteggi online richiedono l'intent **Presence** sul bot. Senza, la risposta lo
dichiara e mostra solo i totali, invece di segnare zero.

---

## Problemi comuni

**I canali non sono stati creati.** Al bot manca **Gestire i canali**, oppure la
categoria che hai scelto non esiste più.

**Un canale è fermo su un numero vecchio.** O il margine di rinomine è esaurito —
aspetta che passi la finestra di dieci minuti — oppure il bot ha perso Gestire i canali
dopo averlo creato.

**Qualcuno ha cancellato uno dei canali.** Il prossimo aggiornamento lo ricrea. Non
serve spegnere e riaccendere la funzione.

**Il contatore staff segna 0.** Nessun ruolo è selezionato, o i ruoli selezionati non
sono quelli che il tuo staff ha davvero.

**`/server stats` non mostra gli online.** L'intent Presence è disattivo nel Developer
Portal di Discord.

---

Avanti: [Livelli](IT-Configurazione-Livelli) · [Log](IT-Configurazione-Log)
