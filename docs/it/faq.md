# FAQ e risoluzione problemi

[English](../faq.md) · **Italiano**

---

## Configurazione

**Il mio server non compare nella dashboard.**
Tre cause possibili: VionDefence non è installato lì, non hai **Gestire il server**
su quel server, oppure la tua sessione Discord è vecchia. Prova prima a uscire e
rientrare — è la causa più comune.

**Ho invitato il bot ma non vedo nessun comando.**
I comandi sono registrati globalmente e la prima volta possono metterci qualche minuto
a propagarsi. Se continuano a non comparire, re-invita il bot assicurandoti che lo scope
`applications.commands` sia incluso.

**Un comando dice che non è attivo.**
È disattivato su quel server. Attivalo nella dashboard sotto **Comandi**. `/ping` è
disattivo di default.

**Un comando dice che non ho i permessi.**
Controlla la riga del comando sotto **Comandi**: potrebbe richiedere un permesso Discord
che non hai, un ruolo di cui non fai parte, oppure essere limitato a canali specifici.
I tre controlli si applicano insieme.

---

## Moderazione

**`/mute` fallisce.**
Quasi sempre per uno di questi due motivi:

1. Non è impostato nessun ruolo mute in **Moderazione**. Impostane uno.
2. Il ruolo mute sta **sopra** il ruolo VionDefence in Impostazioni server → Ruoli.
   Un bot non può assegnare un ruolo più in alto del proprio. Trascina VionDefence
   sopra di esso.

**Non riesco a sanzionare un membro specifico.**
VionDefence si rifiuta di agire su chi è più in alto di lui nella gerarchia dei ruoli,
su sé stesso, e sul moderatore che esegue il comando. Alza il ruolo VionDefence se il
bersaglio è effettivamente sotto di te ma sopra il bot.

**Un ban temporaneo non è stato rimosso.**
Le scadenze vengono controllate ogni 30 secondi mentre il bot è online. Se il bot era
offline al momento della scadenza, viene rimosso poco dopo il riavvio. Se resta
bloccato, verifica che il bot abbia ancora **Bannare membri**.

**Una regola di escalation dei warn non è scattata.**
Le regole confrontano il numero di warn attivi in modo **esatto**. Una regola a soglia 3
scatta solo sul terzo warn attivo — se il membro è passato da 2 a 4 perché nel frattempo
hai anche azzerato e riaggiunto dei warn, non scatta. Controlla il conteggio con
`/userhistory`, e ricorda che i warn scaduti e revocati non sono attivi.

**I membri non ricevono i DM sulle loro sanzioni.**
O la notifica in DM per quel tipo di sanzione è disattivata in **Moderazione**, oppure
il membro ha disattivato i messaggi privati dai membri del server. La sanzione viene
applicata in entrambi i casi.

---

## Automod

**L'automod non intercetta niente.**
Controlla, in ordine: il modulo è **attivo**; il membro non è nei **ruoli esenti** o
negli **utenti esenti**; **rispetta la gerarchia dei ruoli** non lo sta escludendo
perché sta sopra il bot. I bot e i messaggi di sistema vengono sempre ignorati.

**L'automod intercetta troppo.**
Per l'anti-insulti, abbassa la **sensibilità**. Per l'anti-pubblicità, aggiungi domini
ai **domini in whitelist** o disattiva **blocca link** tenendo attivo **blocca inviti
Discord**. Per l'anti-flood, alza i **messaggi massimi** o accorcia l'**intervallo**.

**L'automod rileva ma non sanziona.**
Il modulo è in modalità **passiva**. Passalo a **passiva + attiva** e scegli un'azione.
Un'azione `timeout` senza durata viene saltata.

**Il rilevamento degli insulti è incoerente.**
Alza i **messaggi di contesto** così il classificatore vede più conversazione, e tieni
la modalità passiva abbastanza a lungo da tarare la sensibilità prima di attivare
un'azione.

---

## Canali vocali

**Le stanze non vengono create quando entro nell'hub.**
A VionDefence servono **Gestire i canali** nella categoria di destinazione e
**Spostare membri** sul server. Le categorie di log **Canali template** o **Canali
privati** mostrano l'errore reale.

**Le stanze vengono create ma io resto nell'hub.**
Al bot manca **Spostare membri**.

**Le stanze vuote non vengono eliminate.**
Il bot ha perso **Gestire i canali** sulla categoria, oppure il canale è stato spostato
fuori manualmente.

**`/voice` dice che non possiedo nessun canale.**
Non sei in una stanza privata che possiedi. `/voice` agisce sulla stanza in cui ti trovi
in quel momento, e solo per il suo proprietario. Se il proprietario se n'è andato, usa
`/voice claim`.

**I cambi di privacy non fanno niente.**
Al bot servono **Gestire i ruoli** e **Gestire i canali** per riscrivere i permessi
della stanza.

---

## Ticket

**Il selettore dei ticket è vuoto.**
Tutti i pannelli sono disattivati, oppure non fai parte del **team utente** di nessun
pannello. Un team utente vuoto significa che tutti possono aprire quel pannello — uno
non vuoto lo limita.

**Nessuno riesce a chiudere o prendere in carico i ticket.**
Il **team support** del pannello è vuoto, o i ruoli che conteneva sono stati eliminati.
Un team support vuoto blocca il pannello.

**Ho chiuso un ticket ma non ho ricevuto il transcript.**
O la casella **Salva transcript** era deselezionata nella finestra di chiusura, oppure
il **canale di log** del pannello non è impostato, è stato eliminato, o il bot non può
scriverci.

**Un ticket è stato aperto sul pannello sbagliato.**
`/ticket move panel:<nome>` lo riassegna al team e alla categoria giusti senza perdere
la conversazione.

---

## Log

**Una categoria non registra niente.**
Il suo **canale** è vuoto — è così che si spegne una categoria. Impostane uno.

**Una categoria ha un canale ma continua a non registrare niente.**
Il canale è stato eliminato, non è un canale testuale, il bot non può scrivere o
incorporare link lì, oppure la categoria non è inclusa nel piano del server.

**I timestamp sono nel fuso orario sbagliato.**
Imposta il fuso orario sotto **Generale**. Vale per log, transcript e cronologia.

---

## Lingua

**Il bot risponde nella lingua sbagliata.**
La lingua del bot è un'impostazione **per server** sotto **Generale**, separata dalla
lingua della tua dashboard. Cambiala lì.

---

## Ancora bloccato?

Scrivici sul server Discord di supporto o via email:
https://viondefence.com/contacts
