# Bump ME

[English](../bump.md) · **Italiano**

`/bump` mette il tuo server nella **descrizione Discord del bot** — il testo che tutti
leggono sul profilo del bot, in ogni server in cui si trova. Ci resta per una finestra
estratta a caso tra 12 e 24 ore, poi la descrizione torna normale e il server
successivo puo' prendere lo slot.

Disponibile dal piano **Basic**.

---

## Uno slot per tutti

VionDefence e' una sola applicazione Discord con una sola descrizione, quindi puo'
essere sponsorizzato **un server per volta**. Non e' un'attesa per server: finche' un
server qualsiasi occupa lo slot, `/bump` su tutti gli altri risponde dicendo quando si
libera.

La finestra viene estratta di nuovo a ogni bump, da qualche parte tra 12 e 24 ore,
cosi' lo slot non si riapre a un orario prevedibile che un solo server potrebbe
presidiare.

---

## Cosa dice la descrizione

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

La dashboard mostra entrambe, gia' riempite con il tuo nome e il tuo link, prima che
tu salvi.

## L'attivita' del bot

Mentre il tuo server occupa lo slot, il bot mostra anche un'attivita' — **Playing
on `https://discord.gg/iltuocodice`** — accanto al suo nome in ogni elenco membri,
cosi' la sponsorizzazione si vede senza aprire il profilo del bot.

L'attivita' viene rimossa alla scadenza della finestra, al rilascio anticipato dello
slot e a ogni riavvio: gli stessi momenti in cui torna la descrizione predefinita.

---

## Configurazione

Il pannello **Bump ME** ha una voce sua nella barra laterale della dashboard, sotto
*Promozione*.

| Impostazione | Cosa fa |
|---|---|
| **Attiva Bump ME** | Mentre e' spento `/bump` risponde che la funzione e' disattivata qui |
| **Nome del server** | Il nome scritto nella descrizione. Vuoto usa il nome del server Discord |
| **Link di invito** | Il tuo invito, es. `https://discord.gg/iltuocodice` |
| **XP per l'esecuzione di `/bump`** | XP dati a chi lo ha eseguito. Zero non da' nulla |

Il link di invito dev'essere un vero invito Discord (`discord.gg/…`,
`discord.com/invite/…` o `discordapp.com/invite/…`); qualsiasi altra cosa viene
rifiutata al salvataggio. Non si puo' attivare la funzione senza aver prima impostato
un link: `/bump` potrebbe solo rispondere con un errore.

Usa un invito **senza scadenza**. Il bot non controlla se il link funziona ancora,
quindi uno scaduto resterebbe nella descrizione a non fare nulla per tutta la finestra.

### Il premio in XP

Gli XP arrivano solo se il [sistema di livelli](livelli.md) e' attivo. Passano per la
stessa scala di qualsiasi altro XP: possono far salire di livello il membro, il che
assegna i premi di quel livello e manda la solita notifica.

---

## Eseguirlo

`/bump` e' disponibile a tutti di default; limitalo dalla sezione **Comandi** come
qualsiasi altro comando se preferisci che lo esegua solo lo staff.

| Risposta | Significato |
|---|---|
| Server bumpato | La descrizione porta ora il tuo server, fino all'ora indicata |
| E' sponsorizzato un altro server | Lo slot e' occupato; si libera all'ora indicata |
| Bump ME e' disattivato | Attivalo dalla dashboard |
| Nessun link di invito impostato | Aggiungine uno dalla dashboard |

La conferma mostra il nome, il link e quando si libera lo slot, piu' gli XP guadagnati
quando ce ne sono.

---

## Quando il bot si riavvia

All'avvio la descrizione torna a quella predefinita e lo slot viene liberato, quindi
`/bump` e' subito di nuovo disponibile. Un bump non sopravvive al riavvio del bot.

E' voluto: il bot non puo' continuare a promettere una sponsorizzazione che ha smesso
di mostrare mentre era spento, e lasciare lo slot bloccato fermerebbe ogni server per
ore a causa di un riavvio che nessuno ha chiesto.

---

## Quando finisce un piano

Un server che scende sotto Basic perde la funzione. Se in quel momento occupava lo
slot, la descrizione viene ripristinata e lo slot si libera subito.

Lo stesso vale se il bot viene rimosso da un server che stava occupando lo slot.

---

## Log

I bump e la loro scadenza vengono registrati nella categoria di log **Livelli** — vedi
[Log](log.md). La dashboard tiene inoltre gli ultimi dieci bump del tuo server, con chi
ha eseguito ognuno, quando e quanti XP ha pagato.

---

Avanti: [Log](log.md)
