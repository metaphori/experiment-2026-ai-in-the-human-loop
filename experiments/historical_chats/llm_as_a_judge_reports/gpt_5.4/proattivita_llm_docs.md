# Verifica dei momenti in cui sarebbe stata utile una maggiore proattività del LLM nelle chat di `dataset/docs`

## Perimetro

Questa analisi riguarda le chat contenute in `dataset/docs`.

Per ogni chat ho considerato i turni in sequenza, interpretando i tag così:

- `<human></human>`: richieste o follow-up dell'umano;
- `<LLM></LLM>`: risposte del modello.

L'obiettivo non è individuare errori espliciti, ma verificare **se e quando sarebbe stato utile che il LLM fosse più proattivo**, ad esempio chiedendo:

- dati aggiuntivi;
- chiarimenti sui criteri;
- vincoli di output;
- informazioni tecniche sull'ambiente o sui file.

## Criterio di valutazione

Ho considerato che una maggiore proattività del LLM sarebbe stata utile quando erano presenti una o più di queste condizioni:

1. **criterio di correttezza ambiguo**;
2. **input incompleto per un output molto specifico**;
3. **dipendenza forte da file allegati o da dati non esplicitati nel prompt**;
4. **rischio elevato di allucinare numeri, categorie o assunzioni**;
5. **compito tecnico sensibile all'ambiente di esecuzione**;
6. **richiesta potenzialmente troppo ampia rispetto ai dati effettivamente disponibili**.

Non considero necessaria proattività aggiuntiva quando:

- il task è semplice e ben definito;
- i file allegati rendono il compito già sufficientemente chiaro;
- la risposta diretta è ragionevolmente adeguata senza bisogno di ulteriori vincoli.

## Verdetto sintetico

Sì: **nelle chat analizzate emergono diversi momenti in cui sarebbe stato utile un LLM più proattivo**.

La proattività sarebbe stata particolarmente utile in due classi di situazioni:

- **prima di generare output analitici o contenutistici ad alta interpretazione**;
- **prima di generare codice eseguibile o script dipendenti dall'ambiente**.

In termini pratici, il LLM tende spesso a:

- rispondere subito;
- assumere criteri impliciti;
- colmare da sé i dettagli mancanti;

quando invece sarebbe stato meglio **fermare il flusso per 1-3 domande di chiarimento**.

## Episodi principali in cui la proattività sarebbe stata utile

### 1. `1.1`, turno LLM 2

**Situazione**

L'umano chiede in generale come analizzare risposte aperte di un questionario, anche statisticamente.

**Perché sarebbe servita proattività**

Il LLM risponde subito con una panoramica molto ampia. Sarebbe stato però utile chiedere almeno alcune informazioni preliminari, per adattare il metodo:

- quante risposte aperte ci sono;
- se il questionario contiene anche domande chiuse;
- se l'obiettivo è esplorativo, descrittivo o comparativo;
- se esistono già variabili di sottogruppo da confrontare.

**Domande proattive utili**

- `Quante risposte aperte hai e su quante domande?`
- `Vuoi un metodo rapido per una presentazione o un'analisi più rigorosa da paper?`
- `Hai anche variabili come genere, anno o corso di studi da usare nei confronti?`

**Valutazione**

`Proattività utile: alta`

---

### 2. `1.3`, turno LLM 2

**Situazione**

L'umano fornisce una lunga lista di risposte e chiede una tabella con categorie, frequenze, risposte e sentiment.

**Perché sarebbe servita proattività**

Il task è molto ricco, ma contiene almeno tre ambiguità rilevanti:

- le categorie devono essere **mutuamente esclusive** o una risposta può stare in più categorie?
- la frequenza deve contare le **risposte uniche** o le **menzioni di categoria**?
- il sentiment è davvero una dimensione utile per questa specifica domanda, oppure rischia di essere spurio?

Il LLM infatti risponde assumendo un modello multi-etichetta e specificando solo dopo che la frequenza corrisponde alle menzioni, non alle risposte uniche.

**Domande proattive utili**

- `Vuoi una sola categoria principale per risposta o più categorie per la stessa risposta?`
- `La frequenza deve riferirsi alle risposte o alle occorrenze di categoria?`
- `Preferisci una bozza esplorativa o una codifica più rigorosa e riproducibile?`

**Valutazione**

`Proattività utile: molto alta`

---

### 3. `1.4`, turno LLM 2

**Situazione**

L'umano allega due paper e chiede consigli metodologici per analizzare dati qualitativi e quantitativi del questionario.

**Perché sarebbe servita proattività**

Il LLM assume subito che i paper siano entrambi pertinenti e ne ricava consigli generali. Sarebbe stato utile chiarire:

- se i due paper erano davvero i riferimenti metodologici principali;
- se l'utente voleva un confronto tra i paper o solo consigli applicativi;
- quale fosse la struttura del questionario reale.

In assenza di queste domande, la risposta resta corretta ma generica.

**Domande proattive utili**

- `Vuoi che estragga dai paper un metodo operativo oppure un confronto tra approcci?`
- `Il tuo questionario ha scale Likert, scelte multiple, domande aperte o tutte queste cose insieme?`
- `L'obiettivo finale è una presentazione, un report interno o un paper scientifico?`

**Valutazione**

`Proattività utile: media`

---

### 4. `2.3`, turno LLM 2

**Situazione**

L'umano chiede di riassegnare “correttamente” le categorie nei JSON, mantenendo le categorie esistenti.

**Perché sarebbe servita proattività**

La parola chiave è `correttamente`: il criterio di correttezza non è esplicitato. Il LLM parte invece direttamente con una riclassificazione basata su keyword e precedenze proprie.

Questo è il classico caso in cui sarebbe stato meglio chiedere:

- se esiste un codebook;
- se c'è una distribuzione precedente da rispettare;
- se l'obiettivo è massimizzare coerenza semantica o continuità con l'analisi già fatta.

Il follow-up successivo dell'umano (`La tua riassegnazione ... è allineata rispetto a questa analisi?`) conferma che il criterio implicito non era stato esplicitato abbastanza all'inizio.

**Domande proattive utili**

- `Hai una griglia di codifica o esempi di assegnazione corretta da seguire?`
- `Devo privilegiare la coerenza semantica o l'allineamento con il conteggio precedente?`
- `Le categorie devono restare identiche anche nel significato operativo, o solo nel nome?`

**Valutazione**

`Proattività utile: molto alta`

---

### 5. `3.1`, turno LLM 2

**Situazione**

L'umano chiede come presentare i risultati al gruppo di ricerca, allega JSON, CSV e slide, e apre anche alla possibilità di un codice LaTeX per un paper.

**Perché sarebbe servita proattività**

Il prompt è ricco, ma il task ha almeno tre possibili output diversi:

- struttura per la presentazione orale;
- template o skeleton per il paper;
- revisione delle categorie qualitative.

Il LLM parte su tutto insieme. Sarebbe stato utile prioritizzare con l'utente:

- cosa serve prima;
- quanto deve essere breve la presentazione;
- se i numeri da mostrare sono già verificati o solo provvisori.

Questo avrebbe ridotto il rischio di introdurre numeri o suggerimenti troppo assertivi.

**Domande proattive utili**

- `Preferisci che parta dalla presentazione o dalla struttura del paper?`
- `Quanti minuti durerà l'intervento e quante slide vuoi fare?`
- `I valori numerici che hai allegato sono già verificati o sono ancora da consolidare?`

**Valutazione**

`Proattività utile: alta`

---

### 6. `3.2`, turno LLM 2

**Situazione**

L'umano chiede suggerimenti per una presentazione partendo da analisi grezza, questionario PDF e template slide.

**Perché sarebbe servita proattività**

Il LLM produce subito una scaletta con molti numeri specifici e anche riferimenti a significatività statistica. Sarebbe stato più prudente chiedere:

- se quei numeri andavano calcolati davvero dai file;
- se i valori nelle slide dovevano essere definitivi o segnaposto;
- se il template allegato doveva essere davvero riutilizzato come master grafico.

Il seguito della chat mostra infatti che il template è un vincolo reale e che la gestione dei file PowerPoint non era così lineare.

**Domande proattive utili**

- `Vuoi una scaletta concettuale o una bozza già con numeri definitivi verificati sui dati?`
- `Devo usare davvero il template allegato come base del file PowerPoint?`
- `Hai già deciso quante slide finali vuoi ottenere?`

**Valutazione**

`Proattività utile: molto alta`

---

### 7. `3.3`, turno LLM 2

**Situazione**

L'umano chiede un grafico a barre orizzontali “simile” a uno allegato, partendo dai dati contenuti nell'immagine.

**Perché sarebbe servita proattività**

Questo è un caso tipico in cui il LLM avrebbe dovuto rallentare e chiedere:

- se esistono i dati tabellari originali, invece di ricavarli dall'immagine;
- se l'utente vuole solo il codice o anche il file immagine pronto;
- in quale ambiente eseguirà il codice.

La chat evolve poi in errore di backend Matplotlib su PyCharm, che sarebbe stato parzialmente prevenibile con una domanda iniziale sul contesto di esecuzione.

**Domande proattive utili**

- `Hai i dati grezzi in CSV/JSON/XLSX invece che solo nel grafico?`
- `Vuoi il codice Python o direttamente il file PNG/PDF del grafico?`
- `Lo eseguirai in Jupyter, terminale o PyCharm?`

**Valutazione**

`Proattività utile: molto alta`

---

### 8. `3.4`, turno LLM 2

**Situazione**

Richiesta molto simile alla precedente: creare un grafico a partire da un'immagine e da un altro esempio grafico.

**Perché sarebbe servita proattività**

Anche qui il LLM prova subito a generare codice e valori aggregati. Sarebbe stato utile chiedere:

- se la frequenza di `Altro` era davvero 14 o andava verificata dai dati originali;
- se l'utente voleva un grafico per pubblicazione o solo per uso interno;
- se i dati da aggregare erano tutti noti oppure solo dedotti visivamente.

La dipendenza da stime ricavate dall'immagine rendeva appropriata una breve richiesta di conferma.

**Domande proattive utili**

- `Mi confermi i conteggi esatti da usare, soprattutto per la voce "Altro"?`
- `Vuoi che ricostruisca il grafico da immagine o preferisci passarmi i dati tabellari?`
- `Ti serve un grafico visivamente simile o anche numericamente verificato rispetto ai dati originali?`

**Valutazione**

`Proattività utile: molto alta`

---

### 9. `4.1`, turno LLM 2

**Situazione**

L'umano chiede come si chiamano statisticamente tre variabili che caratterizzano il campione.

**Perché sarebbe servita proattività**

Qui la proattività sarebbe stata utile solo in misura limitata. Il LLM risponde in modo abbastanza diretto e chiaro. Una piccola domanda proattiva avrebbe potuto però migliorare l'aderenza terminologica:

- l'utente sta parlando in senso generale;
- oppure nel contesto specifico di chi-quadro, regressione o ANOVA?

**Domande proattive utili**

- `Ti serve il termine generale o quello più adatto al test statistico che userai?`

**Valutazione**

`Proattività utile: bassa`

---

### 10. `4.2`, turni LLM 2, 6 e 8

**Situazione**

L'umano chiede modifiche a uno script statistico con normalizzazione dei sottogruppi, poi aggiunge richieste su output `XLSX`, cartelle, ordine delle colonne e interpretazione.

**Perché sarebbe servita proattività**

Questa è la chat in cui la proattività mancata pesa di più sul piano tecnico. In più punti il LLM sarebbe stato più efficace se avesse chiesto prima:

- quale versione di `pandas`/`xlsxwriter`/`openpyxl` è installata;
- se l'utente vuole compatibilità massima o solo una soluzione per il proprio ambiente;
- come sono fatti davvero i file di input;
- quali assunzioni statistiche vuole seguire in presenza di celle sparse o frequenze attese nulle.

Il seguito della chat mostra infatti una serie di fix progressivi su:

- generazione `XLSX`;
- gestione di `NaN/inf`;
- firma di `ExcelWriter`;
- nomi dei fogli;
- colonne attese;
- errori di `chi2_contingency`.

Molti di questi cicli sarebbero stati ridotti da 2-3 domande iniziali.

**Domande proattive utili**

- `Puoi dirmi quali versioni di pandas, scipy e xlsxwriter/openpyxl stai usando?`
- `Puoi incollare i nomi reali dei fogli e delle colonne dei file che lo script deve leggere?`
- `In caso di celle con frequenze attese nulle, vuoi saltare il test, aggregare categorie o segnalarlo nel report?`
- `Vuoi che produca uno script robusto per ambienti diversi o tarato sul tuo ambiente locale?`

**Valutazione**

`Proattività utile: massima`

## Pattern trasversali emersi

### 1. Il LLM è poco proattivo quando il criterio di correttezza non è esplicito

Esempi:

- `1.3`
- `2.3`
- `3.1`
- `3.2`

In questi casi il LLM assume da sé:

- schema di codifica;
- interpretazione dei numeri;
- struttura del deliverable;
- priorità tra obiettivi diversi.

### 2. Il LLM è poco proattivo con i file e con i dati allegati

Esempi:

- `3.2` sul template PowerPoint;
- `3.3` e `3.4` su grafici ricostruiti da immagine;
- `4.2` su file `JSON`/`XLSX`/sheet/colonne.

La regola che emerge è semplice:

**più il task dipende da file esterni, più il LLM avrebbe dovuto fare domande di allineamento prima di produrre l'output.**

### 3. La proattività è particolarmente mancata nel codice eseguibile

Nelle chat tecniche il LLM tende a fornire subito una soluzione, ma non sempre verifica:

- ambiente;
- versioni librerie;
- struttura reale dei dati;
- casi limite statistici.

Questo porta a script plausibili ma fragili.

### 4. Nei compiti metodologici il LLM dovrebbe spesso chiedere quale sia il livello di rigore richiesto

In più punti sarebbe stato utile distinguere fra:

- bozza rapida;
- supporto per presentazione;
- analisi rigorosa da paper;
- script riproducibile.

Questa domanda meta-metodologica manca spesso, ma avrebbe migliorato molto l'allineamento.

## Conclusione

Nel corpus di `dataset/docs` ci sono **diversi momenti in cui una maggiore proattività del LLM sarebbe stata chiaramente utile**.

La proattività sarebbe stata utile soprattutto per:

1. chiarire i criteri prima di codificare o ricategorizzare dati qualitativi;
2. chiedere il formato e il livello di verifica dei dati prima di generare numeri o grafici;
3. raccogliere informazioni sull'ambiente prima di produrre codice Python eseguibile;
4. chiarire il tipo di deliverable atteso quando il prompt apre contemporaneamente più strade.

La formula più sintetica è questa:

**il LLM, nelle chat analizzate, è stato spesso reattivo e produttivo, ma non abbastanza proattivo nei momenti in cui avrebbe dovuto chiedere chiarimenti prima di assumere vincoli o dettagli mancanti.**

## Nota metodologica

Questa analisi non dice che il LLM avrebbe dovuto fare domande in ogni chat. Dice invece che, in alcuni snodi specifici, una breve fase di chiarimento avrebbe probabilmente:

- ridotto i cicli successivi di correzione;
- evitato assunzioni arbitrarie;
- migliorato l'aderenza degli output;
- reso più robusta l'interazione umano-LLM.
