# Configurazione — Comandi

[English](Configuration-Commands) · **Italiano**

*Dashboard → il tuo server → **Comandi***

Una scheda per ogni comando slash. L'interruttore sulla scheda accende e spegne il
comando; la **chiave inglese** apre un form a comparsa con i tre controlli di accesso.

---

## I quattro controlli

| Controllo | Dove | Effetto |
|---|---|---|
| **Attivo** | Sulla scheda | Disattiva del tutto il comando su questo server |
| **Permesso** | Nel popup | I permessi Discord che il membro deve avere |
| **Ruoli** | Nel popup | Se non è vuota, solo questi ruoli possono usarlo |
| **Canali** | Nel popup | Se non è vuota, il comando funziona solo in questi canali |

Ruoli e canali sono **liste di ammessi**. Vuoto significa nessuna restrizione — non
"nessuno".

I controlli si combinano con **AND**. Se imposti sia un permesso sia una lista di ruoli,
al membro servono il permesso *e* uno dei ruoli. Se togli ogni permesso, il controllo sui
permessi viene saltato del tutto.

Ognuno dei tre si salva in modo indipendente: c'è un pulsante di salvataggio per blocco,
e si accende solo quando hai davvero cambiato qualcosa.

---

## Valori predefiniti

| Comando | Attivo | Permesso |
|---|---|---|
| `/kick` | sì | Espellere membri |
| `/ban` | sì | Bannare membri |
| `/warn` | sì | Moderare membri |
| `/mute` | sì | Moderare membri |
| `/timeout` | sì | Moderare membri |
| `/userinfo` | sì | Moderare membri |
| `/warnings` | sì | Moderare membri |
| `/userhistory` | sì | Moderare membri |
| `/staffhistory` | sì | Moderare membri |
| `/channel-templates` | sì | Gestire i canali |
| `/voice` | sì | nessuno — tutti |
| `/ticket` | sì | nessuno — tutti |
| `/ping` | **no** | nessuno — tutti |

`/voice` e `/ticket` sono aperti a tutti apposta: sono comandi rivolti ai membri, e
agiscono solo sulla stanza vocale che il membro possiede o sul canale ticket in cui si
trova.

Riferimento completo, opzione per opzione:
[docs/it/comandi.md](https://github.com/SirImperivm/viondefence/blob/master/docs/it/comandi.md).

---

## Due modi per dare accesso allo staff

**Per permesso** — l'impostazione predefinita. Chiunque abbia *Moderare membri* può
warnare. Semplice, e segue i ruoli Discord che hai già senza lavoro extra.

**Per ruolo** — aggiungi il tuo ruolo `Moderatore` alla lista dei ruoli del comando.
Esplicito, e sopravvive a chi rimescola i permessi Discord.

Alla maggior parte dei server bastano i default. Usa la lista dei ruoli quando i tuoi
permessi Discord non esprimono con chiarezza chi sono i moderatori.

---

## Limitare ai canali

Aggiungere canali è il modo per tenere `/voice` fuori dalla chat generale, o per
confinare `/userhistory` al canale staff così la cronologia di un membro non viene mai
tirata fuori in pubblico.

Lasciala vuota se non hai quella necessità specifica: una lista di canali è una cosa in
più da aggiornare quando ristrutturi il server.

---

## Regole di sicurezza che non puoi disattivare

Qualunque cosa configuri, VionDefence si rifiuta di:

- far sanzionare un moderatore da **sé stesso**;
- far sanzionare **il bot** da chiunque;
- agire su un membro che sta **sopra il bot** nella gerarchia dei ruoli.

L'ultima è una regola di Discord, non del bot. Vedi
[Installazione](IT-Installazione#2-sistema-la-gerarchia-dei-ruoli).

---

## Fai così adesso

1. Scorri la lista e verifica che i permessi predefiniti corrispondano a come sono
   organizzati i ruoli del tuo staff.
2. Attiva `/ping` se vuoi avere a disposizione un controllo di latenza.
3. Lascia vuote le liste di ruoli e canali se non hai un motivo preciso.

---

Avanti: **[Canali vocali](IT-Configurazione-Canali-Vocali)**
