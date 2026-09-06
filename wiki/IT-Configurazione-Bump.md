# Configurazione — Bump ME

[English](Configuration-Bump) · **Italiano**

*Dashboard → il tuo server → **Bump ME***

`/bump` scrive il tuo server nella **descrizione Discord del bot** — il testo sul profilo
del bot, visibile da ogni server in cui si trova — e ce lo tiene per 12-24 ore.

Richiede il piano **Basic**. Di default è **spento**.

---

## Prima capisci questo

VionDefence è una sola applicazione Discord con **una sola** descrizione. Non è uno slot
per server: finché un server qualsiasi la occupa, `/bump` ovunque altro risponde dicendo
l'ora in cui si libera.

La finestra viene estratta a caso tra 12 e 24 ore a ogni bump, quindi lo slot non si
riapre mai a un'ora prevedibile che un server potrebbe stare ad aspettare.

---

## Impostalo

1. Incolla un **invito senza scadenza** per il tuo server.
2. Se vuoi, imposta un **nome del server** — lascialo vuoto per usare il nome Discord.
3. Se vuoi, imposta gli **XP per l'esecuzione di `/bump`**.
4. Attiva **Bump ME** e salva.

Il link viene controllato nella forma al salvataggio (`discord.gg/…`,
`discord.com/invite/…` o `discordapp.com/invite/…`) e la funzione non si può attivare
senza.

Crea un invito **che non scade mai**. Il bot non prova il link, quindi un invito da 24
ore incollato qui passerà gran parte della finestra a puntare nel vuoto.

| Impostazione | Significato |
|---|---|
| **Attiva Bump ME** | Mentre è spento `/bump` dice che la funzione è disattivata qui |
| **Nome del server** | Il nome nella descrizione. Vuoto usa il nome Discord |
| **Link di invito** | Dove la descrizione manda le persone |
| **XP per l'esecuzione di `/bump`** | Pagati a chi lo esegue. 0 non paga nulla |

---

## Cosa viene scritto

Mentre il tuo server occupa lo slot:

```
Bot bumped by ${server-name}: ${server-url}

VionDefence Security Protection Managing.
Support Discord: https://discord.gg/CUPvkc87CY
```

Il resto del tempo:

```
VionDefence Security Protection Managing.
Support Discord: https://discord.gg/CUPvkc87CY
```

Il pannello mostra l'anteprima di entrambe con i tuoi valori già dentro, prima che salvi.

---

## Il premio in XP

Pagato solo quando il [sistema di livelli](IT-Configurazione-Livelli) è attivo. Sale la
stessa scala di qualsiasi altro XP, quindi un bump può far superare un livello a qualcuno
e far assegnare i premi di quel livello.

Tienilo basso. Rendere `/bump` il modo più veloce di salire trasforma la classifica in
una gara a chi esegue un comando, che non è quello che la scala dovrebbe misurare.

---

## Chi può eseguirlo

`/bump` è aperto a tutti di default. Limitalo da [Comandi](IT-Configurazione-Comandi) —
per permesso, ruolo o canale — come qualsiasi altro comando.

Valuta di limitarlo a un ruolo. Se ci corrono tutti, lo slot lo prende chi è sveglio in
quel momento, e agli altri la risposta è sempre "occupato, ripassa più tardi".

---

## Riavvii e cambi di piano

**Al riavvio del bot** la descrizione torna a quella predefinita e lo slot viene
liberato, quindi `/bump` funziona di nuovo subito. Un bump non sopravvive a un riavvio.

**Se il piano scende sotto Basic**, o il bot viene rimosso dal server, un bump che stavi
occupando viene rilasciato subito e la descrizione ripristinata.

---

## Come controllarlo

Il pannello mostra se lo slot è libero, occupato da qualcun altro o tenuto da te e fino a
quando. Sotto ci sono i tuoi ultimi dieci bump: chi ha eseguito ognuno, quando e quanti
XP ha pagato.

Bump e scadenze vengono scritti anche nella categoria di log **Livelli**
([Log](IT-Configurazione-Log)).

---

## Problemi comuni

**`/bump` dice che la funzione è disattivata.** È spenta nel pannello, o il piano è sceso
sotto Basic.

**`/bump` dice che non c'è un link di invito.** Il campo del link è vuoto. Visto che la
funzione non si può attivare senza, di solito vuol dire che è stato svuotato dopo.

**"È sponsorizzato un altro server".** Funziona come previsto: uno slot per tutto il bot.
La risposta dice quando si libera.

**Il bump è sparito.** Il bot si è riavviato. Lo slot è di nuovo libero: esegui `/bump`
un'altra volta.

---

Avanti: [Livelli](IT-Configurazione-Livelli) · [Comandi](IT-Configurazione-Comandi)
