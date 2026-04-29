# Valutazione "LLM-as-a-judge" della maturity umano-LLM nella prima fase di analisi del questionario

## Obiettivo

Questo report stima il livello di maturity della diade umano-LLM nella prima fase di analisi del questionario sul settore calzaturiero, usando le chat significative presenti nella cartella `docs` e adottando una lettura coerente con:

- Casadei, Delnevo, Mirri, *Human-Under-Test and Continual Bidirectional Assessment for Co-development of Human-AI Systems*.
- Humphrey, *Managing the Software Process* (modello a cinque livelli: Initial, Repeatable, Defined, Managed, Optimizing).

L'obiettivo non e valutare la correttezza puntuale di ogni conteggio prodotto nelle chat, ma stimare il grado di maturazione della collaborazione tra umano e LLM: quanto l'interazione diventa piu consapevole, strutturata, verificabile e strategica.

## Corpus e materiali usati

### Chat analizzate

Sono stati analizzati 11 documenti `.docx` nella cartella `docs`, per un totale di 30 turni umani e 30 turni LLM:

- `1 - Analisi questionario calzaturiero.docx`
- `2 - Analisi dati questionario.docx`
- `3 - Analisi dataset con LLM.docx`
- `4 - Analisi preliminare questionario.docx`
- `Q1 (OT) - 2.3 - Analisi risposte calzaturiero.docx`
- `Q2 (Y_N) - 1.3.1-1.3.2 - Analisi risposta 1.3.docx`
- `Q3 (SC) - 1.1 - Analisi risposte domanda 1.1.docx`
- `Q3-2 (SC) - 8.4 - Analisi risposte famiglia 8.4.docx`
- `Q4 (MC) - 4.4 - Analisi risposte domanda 4.4.docx`
- `Q5 (Ord) - 1.1 - Analisi distribuzione risposte.docx`
- `Q6 (Lik.Inv) - 8.5 - Analisi item Likert Inv. (Grid).docx`

### Materiali di contesto

- `data/questionario_craftrainer_cleaned.csv`
  - 157 righe
  - 43 colonne
  - presenza del campo `consensus`
- `papers/paper2.pdf`
- `papers/SQM94016FU.pdf`

## Metodo di valutazione

### Perche questa rubric e una inferenza operativa

Il paper di Casadei, Delnevo e Mirri introduce il `User-AI Maturity Model` come modello che valuta la maturita dell'utente nella collaborazione con l'AI in termini di:

- awareness
- adaptability
- strategic competence

Inoltre colloca tale valutazione dentro una cornice di:

- expectation calibration
- task decomposition
- feedback loop
- metacognitive scaffolding
- bidirectional assessment

Il paper, pero, e un position paper: definisce il quadro teorico, ma non fornisce una griglia numerica gia pronta per assegnare direttamente un livello da 1 a 5 a un corpus di chat. Per questo motivo, in questo report il giudizio viene costruito con una rubric operativa derivata dal modello concettuale di Casadei et al. e dai cinque livelli staged di Humphrey.

### Livelli usati

| Livello | Etichetta | Segnali attesi nella collaborazione umano-LLM |
| --- | --- | --- |
| 1 | Initial | uso ad hoc, prompt poco strutturati, aspettative poco calibrate, forte dipendenza dall'output del momento |
| 2 | Repeatable | compaiono pattern ricorrenti di richiesta, prime cautele metodologiche, uso del LLM per compiti delimitati e ripetibili |
| 3 | Defined | workflow esplicito, task decomposition stabile, prompt template per tipologia di item, separazione piu chiara tra lavoro semantico del LLM e pipeline deterministiche |
| 4 | Managed | controlli quantitativi sistematici, metriche di qualita, validazione pianificata, regole a priori per confronti e verifiche |
| 5 | Optimizing | miglioramento continuo basato su feedback strutturato, adattamento reciproco esplicito, scaffolding proattivo e raffinato nel tempo |

### Unita di analisi

La stima e stata costruita osservando quattro aspetti:

1. chiarezza e maturazione della formulazione del problema da parte dell'umano
2. capacita del LLM di calibrare aspettative e ruolo metodologico
3. presenza di workflow ripetibili, template e artefatti riusabili
4. grado di verifica, correzione, controllo statistico e miglioramento del processo

## Evidenze principali emerse dal corpus

### 1. Fase iniziale: dal bisogno generico alla prima calibrazione metodologica

Nelle prime chat il lato umano parte esplicitamente da una posizione novizia: dichiara di non avere molta esperienza nell'analisi di questionari e chiede come "partire da zero". Questo e un chiaro segnale di **Initial**, perche il bisogno iniziale e ancora esplorativo e poco proceduralizzato.

Tuttavia il dialogo non resta a questo livello. Gia nelle prime interazioni compaiono tre elementi di maturazione:

- la richiesta di distinguere tra analisi qualitativa e quantitativa
- l'attenzione ai sottogruppi rilevanti: genere, anno di corso, indirizzo
- la domanda su come usare l'LLM in modo "metodologicamente sensato"

Questi segnali mostrano che la collaborazione esce presto dall'improvvisazione pura. L'umano non tratta il modello come un oracolo generico, ma come uno strumento da inquadrare metodologicamente.

### 2. Calibrazione delle aspettative: il LLM viene spostato da "motore statistico" a assistente di ricerca

Una delle evidenze piu forti del corpus e la costruzione progressiva di una corretta divisione del lavoro:

- il LLM viene usato per audit del dataset, codebook, ricodifica semantica e sintesi delle aperte
- le analisi statistiche vengono progressivamente riconosciute come attivita da affidare a strumenti adeguati e verificabili

Questo punto e centrale rispetto al framework di Casadei et al.: la maturita aumenta quando le aspettative verso l'AI sono calibrate sulle sue capacita reali. Nel corpus questa calibrazione compare in modo esplicito in due direzioni:

- l'umano chiede un uso "utile ma metodologicamente sensato"
- il LLM risponde distinguendo tra interpretazione semantica e calcolo statistico deterministico

Questo e un tratto tipico del passaggio a **Repeatable** e apre la strada a **Defined**.

### 3. Standardizzazione della collaborazione per tipologia di item

Il salto di maturita piu evidente emerge nelle chat dedicate ai singoli item. Qui l'umano non formula piu richieste generiche, ma prompt molto strutturati e ripetibili per:

- domanda aperta
- domanda si/no con follow-up aperto
- scelta singola
- scelta multipla
- scala ordinale
- item Likert a polarita inversa

In questi prompt compaiono istruzioni metodologiche molto precise:

- normalizzare varianti ortografiche
- rispettare l'ordine della scala
- non forzare risposte anomale dentro categorie improprie
- separare risposte combinate nelle opzioni multiple
- usare il follow-up aperto per interpretare un item chiuso
- mantenere l'output leggibile e adatto a un primo report

Questo non e piu un uso solo ripetuto del modello: e un uso **standardizzato per classe di problema**. Qui la collaborazione entra chiaramente in area **Level 3 - Defined**, almeno sul piano del task framing.

### 4. Orientamento al deliverable: slide, grafici e report

La prima fase non resta teorica. L'umano porta il LLM a lavorare verso deliverable concreti:

- sintesi da primo report
- grafici per slide
- confronto con grafici gia prodotti
- script Python riusabile

Questo e importante perche, nel modello di Casadei et al., il processo non e solo dialogo: include output, log e piano di lavoro. Nel corpus il LLM non viene usato solo per "parlare del dataset", ma per produrre artefatti operativi.

La collaborazione quindi non e soltanto conversazionale: diventa progressivamente **procedurale e orientata all'output**.

### 5. Comparsa di un vero feedback loop: il caso del JSON con chiavi duplicate

L'episodio metodologicamente piu maturo del corpus e probabilmente quello legato al JSON delle codifiche delle domande aperte.

La sequenza e significativa:

1. l'umano fornisce un JSON con associazioni risposta -> categoria
2. il LLM produce un primo conteggio
3. l'umano verifica e segnala un disallineamento tra numero di righe viste nell'IDE e numero di casi contati
4. il LLM rianalizza il problema e identifica la perdita di occorrenze dovuta a chiavi duplicate sovrascritte nel formato JSON piatto
5. il LLM propone un formato dati migliore e genera uno script riusabile

Questa sequenza mostra tre cose:

- il lato umano non accetta passivamente l'output del LLM
- il lato LLM e capace di correggere il proprio framing tecnico
- il processo produce un miglioramento strutturale del workflow, non solo una correzione locale

Questo e un indicatore forte di transizione da **Repeatable** a **Defined**, con una prima traccia di logica da **Managed**. Non siamo ancora a livello 4, perche manca una procedura di validazione sistematica, ma la direzione e corretta.

### 6. Consapevolezza crescente del bisogno di analisi statistiche adeguate

Nel corpus emerge chiaramente il passaggio da:

- una prima esigenza di capire "come si fa"

a:

- una richiesta di verificare differenze significative tra sottogruppi

L'umano comincia quindi a riconoscere che:

- non basta la sola lettura descrittiva
- servono test coerenti con il tipo di variabile
- i sottogruppi vanno puliti e definiti prima del confronto

Questo e un segnale di maturazione importante. Tuttavia non basta, da solo, a collocare la diade a **Managed**, perche nel corpus non compare ancora un protocollo statistico esplicito ex ante con:

- soglie decisionali formalizzate
- gestione documentata dei multipli confronti
- strategia stabile di validazione
- audit sistematico degli output LLM

## Tracce documentali piu rilevanti

| Gruppo di chat | Funzione nella traiettoria | Segnale di maturity |
| --- | --- | --- |
| `1 - Analisi questionario calzaturiero.docx` | avvio esplorativo | il bisogno parte da zero ma viene subito trasformato in pipeline di lavoro |
| `2 - Analisi dati questionario.docx` | distinzione metodologica | emerge la separazione tra qualitativo, quantitativo e confronto tra sottogruppi |
| `3 - Analisi dataset con LLM.docx` | calibrazione del ruolo dell'LLM | il modello viene ricollocato come assistente di audit, coding e ipotesi, non come arbitro statistico finale |
| `4 - Analisi preliminare questionario.docx` | orientamento al deliverable e feedback loop | priorita alle slide, correzione del problema delle chiavi duplicate, proposta di script riusabile |
| `Q1-Q6` | standardizzazione domanda-per-domanda | prompt template stabili per aperte, binarie, singole, multiple, ordinali e Likert inversa |
| terzi turni di `Q3`, `Q3-2`, `Q4`, `Q5`, `Q6` | ingresso nella logica dei sottogruppi | il focus si sposta da sola descrizione a differenze significative e pulizia dei gruppi di confronto |

## Valutazione per dimensione

| Dimensione | Evidenza sintetica | Punteggio stimato |
| --- | --- | --- |
| Expectation calibration | l'umano chiede un uso metodologicamente sensato; il LLM distingue bene tra lettura semantica e statistica | 3.0/5 |
| Task decomposition | forte specializzazione dei prompt per tipo di domanda e tipo di output | 3.0/5 |
| Workflow e artefatti riusabili | richieste di grafici, confronto con output propri, script Python, formato dati migliore | 3.0/5 |
| Verifica e data quality | controllo di varianti, missing, outlier, errore sul JSON corretto dopo feedback umano | 2.5/5 |
| Gestione quantitativa del processo | compaiono test e p-value, ma senza protocollo di controllo sistematico | 2.0/5 |
| Bidirectional assessment e scaffolding | il LLM scaffolda bene, ma non mette ancora davvero l'umano "under test" in modo proattivo e strutturato | 2.5/5 |

**Media interpretativa:** circa **2.7/5**

## Giudizio finale di maturity

### Stima complessiva

La stima piu difendibile e:

**Livello prevalente: 2 - Repeatable**  
**Con chiara transizione verso 3 - Defined**

### Perche non Level 1

La collaborazione supera presto l'uso puramente ad hoc, perche:

- le richieste diventano ricorrenti e riconoscibili
- il ruolo del LLM viene progressivamente delimitato
- si consolidano pattern di prompt per classi di item
- compare attenzione esplicita a pulizia dati, sottogruppi e limiti metodologici

### Perche non ancora pienamente Level 3 sull'intera fase

Esistono diversi tratti di **Defined**, ma non sono ancora pienamente stabilizzati su tutto il processo. Manca ancora, in modo esplicito:

- un protocollo unificato e documentato per tutte le analisi
- una distinzione operativa sempre rigorosa tra interpretazione LLM e calcolo deterministico
- una strategia sistematica di revisione umana delle codifiche qualitative
- una documentazione coerente delle decisioni analitiche lungo l'intero percorso

In altre parole: il livello 3 compare chiaramente in alcuni segmenti del corpus, ma non governa ancora in modo uniforme tutta la prima fase.

### Perche non Level 4

Non c'e ancora evidenza di:

- misurazione quantitativa stabile della qualita degli output LLM
- validazione campionaria o inter-rater pianificata delle codifiche
- metriche di affidabilita del processo
- controllo sistematico dei falsi positivi nelle analisi per sottogruppi
- ciclo di miglioramento formalizzato con criteri di accettazione

Quindi la collaborazione e gia matura abbastanza da essere ripetibile e in parte definita, ma non ancora gestita in senso quantitativo.

## Lettura sintetica della traiettoria

| Fase del corpus | Carattere dominante | Livello prevalente |
| --- | --- | --- |
| Avvio esplorativo | capire il problema, capire il dataset, capire come usare l'LLM | 1 -> 2 |
| Prima strutturazione metodologica | distinguere qualitativo/quantitativo, fissare una pipeline leggera per la presentazione | 2 |
| Analisi per tipologia di item | prompt template stabili, output attesi chiari, attenzione al trattamento corretto delle variabili | 3 locale |
| Verifica e riuso | controllo errori, revisione del formato dati, script riusabile, attenzione ai sottogruppi | 3 locale, con primi segnali pre-4 |

## Interpretazione sostantiva

Dal punto di vista del rapporto umano-LLM, la prima fase non descrive una dipendenza cieca dal modello. Descrive piuttosto una **co-evoluzione pragmatica**:

- l'umano passa da un bisogno generico a una domanda metodologicamente piu raffinata
- il LLM funziona come scaffold cognitivo e metodologico
- il processo si traduce gradualmente in template, grafici, script e controlli

La maturity quindi non sta solo nel fatto che "il modello risponde bene", ma nel fatto che **l'umano impara a usarlo in modo piu consapevole, delimitato e strategico**.

Questo punto e pienamente coerente con la prospettiva di Casadei et al.: la collaborazione matura quando migliorano insieme:

- il framing del compito
- la calibrazione delle aspettative
- la qualita del feedback
- la capacita di trasformare l'interazione in processo

## Come passare da 2/3 a 3/4 nelle fasi successive

Per alzare il livello di maturity nelle fasi successive, le mosse piu efficaci sarebbero:

1. formalizzare un protocollo stabile domanda-per-domanda
   - tipo variabile
   - pulizia prevista
   - output LLM atteso
   - controllo deterministico previsto

2. separare sempre in modo esplicito:
   - cosa fa il LLM
   - cosa viene calcolato da Python/R
   - cosa viene validato dal ricercatore

3. introdurre una checklist di validazione minima per ogni analisi
   - coerenza dei denominatori
   - trattamento missing
   - regole di ricodifica
   - verifica campionaria delle codifiche qualitative

4. registrare in modo consistente le decisioni analitiche
   - esclusioni
   - accorpamenti
   - test scelti
   - motivazioni metodologiche

5. usare l'LLM anche in modalita piu vicina al "human-under-test"
   - far emergere attivamente dubbi, bias possibili, assunzioni implicite
   - chiedere al modello di interrompere il flusso quando manca un criterio esplicito

## Conclusione

La prima fase di analisi mostra una collaborazione umano-LLM **piu matura di un uso occasionale o ingenuo**, ma **non ancora pienamente gestita come processo quantitativamente controllato**.

La formulazione piu accurata, in termini di maturity, e quindi:

**la diade umano-LLM si colloca prevalentemente al Level 2 (Repeatable), con una transizione ben visibile verso Level 3 (Defined).**

Se il criterio di lettura privilegia i segmenti piu evoluti del corpus, soprattutto quelli con prompt standardizzati, correzione del JSON e produzione di script riusabili, si puo anche dire che:

**la punta piu avanzata della prima fase raggiunge un Level 3 locale, ma l'intera fase nel suo complesso non e ancora oltre il confine tra 2 e 3.**

## Limiti della valutazione

- La valutazione e retrospettiva e basata solo sulle chat selezionate.
- I blocchi `<python/>` sono stati rimossi da parte del corpus, quindi alcuni passaggi esecutivi sono solo indirettamente osservabili.
- Il paper di Casadei et al. e concettuale: la rubric adottata qui e un'operazionalizzazione interpretativa, non uno strumento ufficiale gia validato.
- Il giudizio riguarda la maturity della collaborazione, non la validita definitiva dei risultati statistici o qualitativi prodotti durante la fase.

## Riferimenti

- Roberto Casadei, Giovanni Delnevo, Silvia Mirri, *Human-Under-Test and Continual Bidirectional Assessment for Co-development of Human-AI Systems*, HAIC'25, CEUR Workshop Proceedings. Fonte locale: `papers/paper2.pdf`.
- W. S. Humphrey, *Managing the Software Process*, Addison-Wesley, 1989. Per i cinque livelli staged e stata usata anche la sintesi locale in `papers/SQM94016FU.pdf`.
