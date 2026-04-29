# Valutazione di Maturity umano-LLM della prima fase di analisi del questionario

## Perimetro

Questa valutazione considera come corpus principale le chat in `dataset/docs/1.1`-`1.4`, `2.1`-`2.3`, `3.1`-`3.5`, `4.1`-`4.2`.

Il riferimento teorico è `dataset/papers/paper2.pdf` di Casadei, Delnevo e Mirri, letto insieme al richiamo al maturity model di Humphrey (`dataset/papers/SQM94016FU.pdf`). Il file `dataset/data/questionario_craftrainer_cleaned.csv` è stato usato solo come controllo minimo di coerenza del campione: 157 righe totali, 147 questionari con consenso valido (`Sì`).

## Metodo LLM-as-a-judge

Applico un giudizio qualitativo strutturato di tipo `LLM-as-a-judge` sulle interazioni, trattando ogni chat come evidenza del livello di maturazione della collaborazione umano-LLM.

Il paper di Casadei, Delnevo e Mirri non fornisce ancora una scala operativa pronta all'uso con soglie numeriche definitive. Per questo motivo, in questa analisi operazionalizzo il modello in modo inferenziale, combinando:

- le dimensioni esplicite del paper: `Expectation Calibration`, `User Task Maturity Model`, `User-AI Maturity Model`, `AI Maturity Model`, feedback loop e scaffolding;
- la scala a cinque livelli derivata dal maturity model di Humphrey:
  - `Livello 1 - Initial`
  - `Livello 2 - Repeatable`
  - `Livello 3 - Defined`
  - `Livello 4 - Managed`
  - `Livello 5 - Optimizing`

### Criterio interpretativo adottato

`Livello 1 - Initial`: uso ad hoc del LLM, obiettivi ancora poco formalizzati, fiducia o diffidenza non governate da un processo.

`Livello 2 - Repeatable`: emergono pattern riutilizzabili di prompting e di uso degli output, ma il controllo metodologico resta parziale e dipende ancora molto dal caso specifico.

`Livello 3 - Defined`: il flusso di lavoro umano-LLM è esplicito, più standardizzato, con ruoli, output e passaggi abbastanza chiari.

`Livello 4 - Managed`: il processo è misurato, verificato e governato con controlli sistematici sui risultati e sulla qualità dell'interazione.

`Livello 5 - Optimizing`: esiste miglioramento continuo del sistema umano-LLM tramite feedback espliciti, auditing, metriche e raffinamento stabile del processo.

## Evidenze principali emerse dalle chat

### 1. Fase iniziale: orientamento metodologico

Nelle chat `1.1` e `1.2` l'umano usa il LLM soprattutto per capire "come si fa" l'analisi di un questionario con domande aperte e per distinguere qualitativo e quantitativo. Il LLM svolge una funzione di orientamento generale e di alfabetizzazione metodologica.

Segnale di maturity: basso ma positivo. La collaborazione è ancora `ad hoc`, però inizia la calibrazione delle aspettative. L'umano comprende che le domande aperte richiedono prima codifica qualitativa e poi, eventualmente, passaggi quantitativi.

Stima locale: tra `Livello 1` e inizio `Livello 2`.

### 2. Primo uso operativo sui dati reali

Nella chat `1.3` l'umano passa da una domanda generica a un prompt molto più strutturato: definisce colonne attese, categorie, frequenze, dettaglio delle risposte, sentiment e perfino la classe `NC`.

Questo è un passaggio importante: il LLM non viene più usato solo come "spiegatore", ma come componente operativa del workflow. Tuttavia l'output resta ancora fragile: il modello produce una tabella molto estesa, con segnali di incertezza e con una semantica delle categorie non ancora veramente stabilizzata.

Segnale di maturity: compare una procedura ripetibile di lavoro con il LLM, ma non ancora una procedura definita e controllata.

Stima locale: `Livello 2 - Repeatable`.

### 3. Ricerca di ancoraggio metodologico esterno

Nella chat `1.4` l'umano prova a fondare meglio il lavoro chiedendo consiglio "a partire da due paper". Questo è un segnale importante di crescita: il LLM non viene più interpellato come unica fonte, ma come mediatore tra letteratura e compito.

Il limite è che la risposta del LLM resta piuttosto generale e non costruisce ancora un protocollo esplicito di validazione.

Segnale di maturity: maggiore consapevolezza epistemica dell'umano, ma ancora senza piena governabilità del processo.

Stima locale: `Livello 2`.

### 4. Costruzione di artefatti intermedi e manipolazione dei dati

Le chat `2.1`, `2.2` e `2.3` mostrano un netto avanzamento. Il LLM viene usato per:

- fondere file JSON;
- contare categorie;
- riclassificare risposte con regole più esplicite;
- confrontare nuove categorie con una distribuzione precedente.

Qui emerge un tratto tipico del `Livello 2 avanzato`: l'umano ha capito che il LLM è utile quando gli si chiedono trasformazioni ben delimitate su input strutturati. Nella `2.3` si vede anche un embrione di `Livello 3`, perché compaiono regole di assegnazione, precedenze tra categorie e confronto tra versione vecchia e nuova.

Il limite, però, resta forte: le regole sono ancora costruite dentro la singola chat, non come codebook stabile e versionato.

Stima locale: tra `Livello 2` e `Livello 3`.

### 5. Preparazione della presentazione e del primo report

Nelle chat `3.1` e `3.2` la collaborazione diventa più ambiziosa. L'umano chiede una struttura di presentazione, un impianto da paper, categorie qualitative migliori, grafici, possibili confronti tra sottogruppi.

Questa fase mostra una maturazione reale del lato umano:

- gli obiettivi sono più chiari;
- i deliverable sono espliciti;
- il LLM viene usato come supporto alla progettazione del report, non solo alla risposta puntuale.

Ma proprio qui emerge anche il principale limite di maturity dell'intero sistema umano-LLM: il modello produce, nelle slide suggerite, numeri molto specifici, percentuali e perfino p-value, senza che nella chat sia sempre visibile la catena di giustificazione o il calcolo riproducibile che li sostiene.

Questo punto è decisivo. La collaborazione appare più fluida, ma non ancora veramente `managed`. In altri termini: cresce la produttività, non cresce allo stesso ritmo il controllo epistemico.

Stima locale: `Livello 2 avanzato`, con tratti di `Livello 3` sul piano organizzativo ma non ancora sul piano del controllo.

### 6. Chat di confine verso la fase statistica

Nelle chat `4.1` e soprattutto `4.2` si vede il passaggio più netto verso una maturità superiore. L'umano:

- identifica le variabili di sottogruppo come fattori analitici;
- impone regole di normalizzazione per genere, anno e corso;
- richiede cartelle di output, report per domanda e file `XLSX` riepilogativi;
- tratta il LLM come co-sviluppatore di uno script statistico, non più come semplice risponditore.

Questa è la parte del corpus più vicina a `Livello 3 - Defined`, perché il processo comincia ad avere:

- input attesi;
- regole di trasformazione;
- output previsti;
- struttura di reporting.

Resta però assente un controllo sistematico su assunzioni statistiche, qualità delle categorie, validazione indipendente degli output del LLM e tracciamento delle decisioni.

Stima locale: `Livello 3` basso.

## Valutazione per dimensioni

| Dimensione | Osservazione sintetica | Valutazione |
| --- | --- | --- |
| `Expectation Calibration` | L'umano impara progressivamente cosa chiedere al LLM e quando il LLM è utile; il LLM però raramente esplicita in modo proattivo i propri limiti metodologici. | `2/5` |
| `User Task Maturity` | Il compito passa da domanda vaga a pipeline con categorie, file, script, sottogruppi e report. | `3/5` |
| `User-AI Maturity` | L'umano usa il LLM in modo sempre più strategico e finalizzato, ma non separa ancora nettamente esplorazione, produzione e validazione. | `3/5` |
| `AI Maturity / Scaffolding` | Il LLM è versatile e produttivo, ma poco "critico": spinge poco su verifiche, assunzioni, limiti e richieste di chiarimento. | `2/5` |
| `Feedback Loop / Co-development` | Esiste una chiara co-evoluzione tra umano e LLM nell'arco delle chat; il loop è però implicito, non governato da metriche o audit trail. | `3/5` |
| `Measurement / Validation` | Il controllo dei risultati esiste solo in forma parziale e non sistematica; la validazione forte arriva tardi e resta incompleta. | `2/5` |

Media interpretativa: circa `2.5/5`.

## Stima complessiva del livello di maturity

### Verdetto

La stima complessiva per la prima fase è:

**`Livello 2 - Repeatable`, in transizione verso `Livello 3 - Defined`.**

### Motivo della scelta

La collaborazione non è più `Initial`, perché:

- l'umano sviluppa pattern di prompting riutilizzabili;
- il LLM viene impiegato su compiti sempre più concreti;
- emergono artefatti intermedi stabili come JSON, categorie, script, report e cartelle di output;
- nella parte finale della fase compare una vera decomposizione del problema per sottogruppi e deliverable.

Tuttavia non considero la fase già pienamente `Defined`, perché:

- il processo non è ancora formalizzato in un protocollo unico e stabile;
- la scelta del modello LLM cambia in modo pragmatico, ma non secondo una policy esplicita;
- le categorie qualitative vengono più volte ridefinite senza un codebook consolidato e versionato;
- mancano passaggi sistematici di verifica indipendente prima di promuovere l'output del LLM a risultato da presentare;
- alcune risposte del LLM diventano molto assertive sul piano statistico senza che, nella chat, sia sempre visibile il calcolo riproducibile sottostante.

### Lettura dinamica

Se la maturity venisse stimata non sull'intera prima fase ma sul suo punto finale, la stima sarebbe più alta:

- inizio fase: `Livello 1-2`;
- parte centrale: `Livello 2`;
- confine con la fase statistica: `Livello 3` basso.

Quindi la prima fase non è statica: è una traiettoria di maturazione, non un livello uniforme.

## Punti di forza della collaborazione umano-LLM

- Il LLM ha funzionato bene come acceleratore di comprensione iniziale.
- L'umano ha imparato rapidamente a rendere le richieste più strutturate.
- La collaborazione è diventata produttiva nella costruzione di artefatti intermedi.
- Si osserva una crescita reale della competenza metacognitiva dell'umano: da "non l'ho mai fatto" a "normalizza i sottogruppi, salva in `reports/Qx.y`, genera `XLSX` riepilogativi".

## Limiti che abbassano la maturity

- Confine ancora poroso tra output esplorativi e risultati presentabili.
- Validazione metodologica non sistematica.
- Assenza di un codebook qualitativo stabile con versionamento e criteri di decisione.
- Assenza di un audit trail che registri per ogni risultato: prompt, modello, input, output, verifica e decisione finale umana.
- Limitata capacità del LLM di fare vera funzione di `cognitive mirror` critico: il modello aiuta molto a produrre, meno a rallentare quando sarebbe opportuno verificare.

## Come passare al livello successivo

Per arrivare in modo solido a `Livello 3 pieno` e poi a `Livello 4`, consiglierei di introdurre un protocollo esplicito di collaborazione umano-LLM:

1. Separare sempre tre momenti: `esplorazione`, `produzione`, `validazione`.
2. Stabilire un codebook versionato per le domande aperte, con esempi inclusi/esclusi.
3. Richiedere uno script riproducibile per ogni numero che finirà in slide o report.
4. Tenere un registro delle decisioni: chat usata, modello, prompt, output accettato o scartato, motivo.
5. Introdurre controlli sistematici: campionamento manuale delle codifiche, accordo inter-valutatore, verifica delle assunzioni dei test statistici.
6. Usare il LLM anche come strumento di contestazione controllata: chiedergli non solo "proponi", ma anche "quali sono i punti deboli di questa inferenza?".

## Conclusione

Nella prima fase l'interazione umano-LLM mostra una maturazione reale e osservabile. Non si tratta più di un uso ingenuo del modello, ma nemmeno di una collaborazione già governata con piena disciplina metodologica.

La formula più fedele ai dati è quindi:

**collaborazione a `Livello 2 - Repeatable`, con chiara traiettoria evolutiva verso `Livello 3 - Defined`.**

## Nota sulla confidenza della stima

Confidenza della stima: `media`.

Il giudizio è abbastanza robusto perché la traiettoria delle chat è coerente. La confidenza non è alta al massimo livello perché:

- alcune chat contengono allegati il cui contenuto non è sempre completamente visibile nel transcript;
- in alcuni casi il codice Python può essere stato parzialmente sostituito o sintetizzato;
- il paper di riferimento propone soprattutto un quadro concettuale, non ancora una rubrica di scoring pienamente standardizzata.
