# La dashboard

[English](../dashboard.md) · **Italiano**

Tutto quello che fa VionDefence si configura dalla dashboard web su
https://viondefence.com/dashboard. I comandi slash sono una scorciatoia sopra le
stesse impostazioni.

---

## Come si entra

Accedi con Discord. Il selettore dei server elenca tutti i server dove **entrambe** le
condizioni sono vere:

- hai il permesso **Gestire il server**, e
- VionDefence è installato.

Scegline uno per aprirne la configurazione. Le modifiche hanno effetto immediato — non
c'è un passaggio di pubblicazione separato e non serve riavviare nulla.

---

## Sezioni

### Generale

Lingua, fuso orario, formato data e formato ora del server.

La **lingua** impostata qui è quella dei messaggi che il bot invia *in quel server*. È
indipendente dalla lingua della dashboard, che segue la tua preferenza personale.

Disponibili: Italiano (`it-IT`) e English (`en-US`).

### Comandi

Una riga per ogni comando slash, con quattro controlli ciascuna: **attivo**,
**permesso richiesto**, **ruoli ammessi**, **canali ammessi**.

Riferimento completo e valori predefiniti: [Comandi](comandi.md#permessi-e-restrizioni).

### Canali template

I template dei canali vocali — canale hub, categoria di destinazione, formato del nome
e limite utenti. Vedi [Canali vocali](canali-vocali.md#canali-template).

### Canali privati

Il sistema delle stanze personali — on/off, canale hub, categoria.
Vedi [Canali vocali](canali-vocali.md#canali-privati).

### Ticket

I pannelli dei ticket: categorie, team, moduli, transcript.
Vedi [Ticket](ticket.md).

### Moderazione

Il ruolo mute, le notifiche in DM per ogni tipo di sanzione, la scadenza dei warn e le
regole di escalation. Vedi [Moderazione](moderazione.md).

### Log

Canale di destinazione, colore dell'embed e thumbnail per ognuna delle nove categorie
di log. Vedi [Log](log.md).

### Automod

I tre moduli di automod, le loro soglie e le modalità di azione, più le liste di
esenzione condivise. Vedi [Automod](automod.md).

### Filtro contenuti

Regole per canale su **quali tipi di contenuto possono essere inviati**: testo, file,
immagini e link. I canali che non elenchi continuano ad accettare tutto.

Ogni canale filtrato ha la sua combinazione: un canale può consentire file e immagini
ma non il testo semplice, oppure testo e immagini ma non i link, e così via.

Il testo allegato a un file o a un'immagine viene considerato una **didascalia**: resta
consentito anche quando il testo è filtrato, purché stia entro **1024 caratteri**.

I thread ereditano il filtro del canale da cui sono nati. I ruoli e i membri esenti non
vengono mai filtrati e, finché è attivo *rispetta la gerarchia dei ruoli*, non lo sono
nemmeno il proprietario del server e chi sta sopra il bot.

Un messaggio bloccato viene semplicemente **eliminato** e il suo autore riceve un
**messaggio privato** che spiega cosa è consentito in quel canale. Il filtro contenuti
non applica mai warn, mute, kick o ban: la rimozione viene solo scritta nella categoria
di log **Filtro contenuti**. Il DM si può disattivare, e in quel caso il messaggio viene
rimosso in silenzio.

Richiede il piano **Pro**.

### Livelli

Il sistema di XP e livelli: quanto valgono un messaggio e un minuto in vocale, quali
canali contano, quanto costa ogni livello e cosa assegna ciascuno.

La curva dei livelli si scrive come **formula** — la dashboard mostra i primi dieci
livelli che produce mentre scrivi, così una curva inutilizzabile viene intercettata
prima del salvataggio. Sotto la configurazione stanno i **premi** (un ruolo e una
gratifica testuale per livello) e la **classifica** di chi ha guadagnato di più.

Dettagli completi: [Sistema di livelli](livelli.md).

Incluso dal piano **Free**.

### Bump ME

Ha una voce sua sotto *Promozione*, perché non configura il tuo server: configura il
modo in cui il bot lo pubblicizza altrove.

`/bump` scrive il nome e l'invito del tuo server nella **descrizione Discord del bot**
per una finestra estratta a caso tra 12 e 24 ore. Può occuparla un server per volta. Il
pannello mostra se lo slot è libero, entrambe le versioni della descrizione così come
si leggeranno, e gli ultimi dieci bump del tuo server.

Dettagli completi: [Bump ME](bump.md).

Richiede il piano **Basic**.

### Cronologia

Tutte le sanzioni mai emesse sul server, filtrabili. Da qui puoi:

- aprire il **dettaglio di una sanzione** — moderatore, destinatario, date, motivo,
  stato, e l'azione di revoca;
- aprire il **profilo di un membro** — tutto quello che ha collezionato in un posto solo.

Mostra anche i log dell'automod, così puoi controllare cosa hanno intercettato i filtri.

---

## Account

Fuori dalla dashboard del singolo server, l'area **Account** riguarda te e non un
server:

- **Personale** — i dati del tuo profilo.
- **Accesso** — email, password e il collegamento tra account e Discord.
- **Abbonamenti** — i tuoi piani attivi e i server a cui sono associati.

Puoi accedere con Discord oppure con email e password, e collegare i due in modo che
funzionino entrambi.

---

## Piani

Alcune funzioni e alcuni limiti — quanti template di canale, quanti pannelli ticket,
quanti premi dei livelli, quali categorie di log — dipendono dal piano associato al
server.

Piani attuali e cosa include ciascuno: https://viondefence.com/pricing

Un piano è assegnato a un server specifico. Cambiare il server coperto da un piano, o
cambiare piano, si fa da **Account → Abbonamenti**.

---

Avanti: [Comandi](comandi.md)
