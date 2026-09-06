# Installazione

[English](Installation) · **Italiano**

Invitare il bot, dargli quello che gli serve, ed entrare nella dashboard.

---

## 1. Invita il bot

Apri [viondefence.com](https://viondefence.com) e usa il pulsante **Aggiungi il
bot**. Discord ti chiederà su quale server installarlo, ed elencherà solo i server dove
hai **Gestire il server**.

Accetta i permessi che Discord propone. Ognuno ha un motivo:

| Permesso | Senza di esso |
|---|---|
| **Gestire i canali** | Niente canali vocali temporanei, niente canali ticket |
| **Gestire i ruoli** | I mute falliscono, i permessi dei ticket non vengono scritti |
| **Espellere membri** | `/kick` e l'azione kick dell'automod falliscono |
| **Bannare membri** | `/ban` fallisce, e i ban temporanei non scadono mai |
| **Modera membri** | `/timeout` fallisce |
| **Spostare membri** | Le stanze vocali vengono create ma nessuno ci viene spostato dentro |
| **Inviare messaggi / Incorporare link** | Niente embed di log, niente pannelli ticket |
| **Leggere la cronologia messaggi** | I transcript dei ticket escono vuoti |

Puoi darne di meno, e il resto del bot continua a funzionare — si rompe solo la funzione
interessata. Si rompe però *in silenzio* dal punto di vista dei membri: l'errore finisce
nella categoria di log **Generale**, che è un motivo in più per
[impostare subito i log](IT-Configurazione-Log).

---

## 2. Sistema la gerarchia dei ruoli

È il passaggio che si salta, e su cui poi si perde un'ora a fare debug.

Apri **Impostazioni server → Ruoli** e trascina il ruolo **VionDefence** in alto, sopra
ogni ruolo su cui dovrà agire.

Discord applica due regole che nessun permesso può aggirare:

- un bot non può espellere, bannare, mutare o mettere in timeout chi ha il ruolo più alto
  **sopra** il proprio;
- un bot non può **assegnare** un ruolo che sta sopra il proprio.

Quindi se il ruolo mute finisce sopra VionDefence, ogni `/mute` fallisce. Se i tuoi
moderatori stanno sopra VionDefence, l'automod non potrà mai agire su di loro — cosa
che a volte è proprio quello che vuoi, ed è il senso dell'opzione *Rispetta la gerarchia
dei ruoli* in [Automod](IT-Configurazione-Automod).

Posizione sicura: subito sotto i ruoli di amministrazione, sopra tutto il resto.

---

## 3. Apri la dashboard

Vai su [viondefence.com/dashboard](https://viondefence.com/dashboard) e accedi con
Discord.

Vedrai tutti i server dove **entrambe** le condizioni sono vere:

- hai **Gestire il server**, e
- VionDefence è installato.

Clicca su uno per aprirne la configurazione. La barra laterale elenca le sezioni; ognuna
ha la sua pagina in questa wiki.

### Se il tuo server non compare

| Causa | Soluzione |
|---|---|
| Il bot non è su quel server | Rifai il passo 1 e scegli quel server |
| Non hai Gestire il server | Chiedi al proprietario di dartelo, o di fare la configurazione |
| La sessione Discord è vecchia | Esci dalla dashboard e rientra — è la causa più comune |

---

## 4. Verifica che i comandi siano arrivati

Su Discord, scrivi `/` in un canale qualsiasi. Dovresti vedere i comandi di
VionDefence.

I comandi slash sono registrati **globalmente**, quindi la prima volta possono metterci
qualche minuto a propagarsi. Se dopo non compaiono ancora, re-invita il bot assicurandoti
che l'invito includa lo scope `applications.commands` — un invito con il solo scope `bot`
installa il bot senza i suoi comandi.

---

## Account e collegamento

Puoi accedere con Discord, oppure con email e password, e collegare i due in modo che
funzionino entrambi. Sta sotto **Account → Accesso** e non riguarda nessun server in
particolare.

I piani sono associati a un server specifico e si gestiscono da **Account →
Abbonamenti**. Quali funzioni e quali limiti ha un server — quanti template vocali,
quanti pannelli ticket, quali categorie di log — dipende da quel piano. Piani attuali:
[viondefence.com/pricing](https://viondefence.com/pricing).

---

Avanti: **[Configurazione generale](IT-Configurazione-Generale)**
