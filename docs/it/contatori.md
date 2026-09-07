# Contatori dei membri

[English](../counters.md) · **Italiano**

Canali vocali che mostrano quante persone ci sono sul server, tenuti aggiornati da
soli. Tutti li vedono, nessuno ci entra: sono cartelli, non stanze.

Disponibile dal piano **Free**.

---

## Cosa viene creato

Attivando la funzione nascono tre canali vocali:

| Canale | Conta | Segnaposto |
|---|---|---|
| Tutti | Ogni membro, bot compresi | `{total-count}` |
| Bot | Solo i bot | `{bots-count}` |
| Membri | Tutti tranne i bot | `{members-count}` |

Un **quarto** canale è facoltativo e conta lo staff, in base a un elenco di ruoli che
scegli tu: `{staff-count}`. Chi ha almeno uno di quei ruoli viene contato una volta
sola.

Ogni canale nasce con `Vedi canale` consentito e `Connetti` negato per `@everyone`,
quindi si vede nell'elenco ma non ci si entra.

Disattivando la funzione i canali vengono eliminati. Non si perde nulla: i numeri
vengono letti da Discord ogni volta, non sono mai salvati.

---

## I nomi

Il nome lo decidi tu; viene sostituito solo il segnaposto.

```
👥 Tutti: {total-count}      →      👥 Tutti: 1247
🛡 Staff: {staff-count}       →      🛡 Staff: 9
```

Un nome deve contenere il proprio segnaposto — altrimenti la dashboard lo rifiuta,
perché un contatore che non cambia mai è solo un canale con un nome fuorviante. I nomi
sono tagliati ai 100 caratteri consentiti da Discord.

---

## Ogni quanto si aggiorna

**Discord consente due rinomine di canale ogni dieci minuti.** Oltre quella soglia la
richiesta non viene rifiutata, viene messa in coda: un contatore impostato per
aggiornarsi ogni minuto resterebbe indietro in silenzio, proprio mentre sembra il più
aggiornato di tutti.

Per questo l'intervallo ha un minimo di **cinque minuti** e di default è dieci. Il bot
salta anche la rinomina quando il nome nuovo è identico a quello attuale, così un
server tranquillo non consuma il proprio margine per niente.

---

## `/server stats`

Manda gli stessi numeri come messaggio effimero, visibile solo a chi lo esegue, e
**ricalcola sul momento**: non legge i nomi dei canali.

Dice inoltre quanti di quei membri e di quello staff sono **online**, cosa che i canali
non possono mostrare.

| Opzione | Obbligatoria | Descrizione |
|---|---|---|
| *(nessuna)* | | `/server stats` non ha opzioni |

Il comando funziona sia con i canali contatore attivi sia senza: con quelli attivi ne
approfitta anche per riallinearli.

I conteggi online richiedono l'intent **Presence** di Discord. Senza, il comando lo
dichiara nel piè di pagina e mostra solo i totali, invece di segnare zero — che sarebbe
un numero sbagliato, non un numero basso.

---

## Permessi

A VionDefence serve **Gestire i canali** per creare, rinominare ed eliminare i
contatori. Se perde quel permesso i canali restano come sono, con gli ultimi numeri
scritti.

Metti i canali in una categoria se li vuoi raggruppati, oppure lascia la categoria
vuota per averli in cima al server.

---

Avanti: [Sistema di livelli](livelli.md)
