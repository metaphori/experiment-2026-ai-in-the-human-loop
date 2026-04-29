# Stima del livello di Maturity umano-LLM nella prima fase di analisi del questionario

## Obiettivo

Stimare, con un approccio "LLM-as-a-judge", il livello di maturity della collaborazione tra l'umano e ChatGPT nella prima fase di analisi del questionario, cioe nel periodo compreso tra l'11 aprile 2025 e il 7 maggio 2025.

## Base teorica usata

La stima si basa su due riferimenti:

1. il paper di Casadei, Delnevo e Mirri, *Human-Under-Test and Continual Bidirectional Assessment for Co-development of Human-AI Systems*;
2. la logica dei livelli di maturity derivata da Humphrey, richiamata dal paper.

### Nota metodologica importante

Il paper di Casadei, Delnevo e Mirri non fornisce una rubrica operativa gia pronta con punteggi e soglie per assegnare un livello numerico univoco al rapporto umano-LLM. Fornisce invece un quadro concettuale utile per osservare:

- expectation calibration;
- task decomposition;
- user task maturity;
- user-AI maturity;
- AI maturity come capacita di supporto adattivo;
- feedback, nudging e scaffolding metacognitivo;
- co-reasoning loop e co-evoluzione.

Per questo motivo la stima seguente e una **operazionalizzazione interpretativa**: uso i 5 livelli classici di Humphrey come griglia e li adatto al caso della collaborazione tra un ricercatore principiante rispetto al compito e un LLM generalista.

## Adattamento dei livelli di Humphrey al caso umano-LLM

### Livello 1. Initial

La collaborazione e ad hoc, esplorativa e reattiva. L'utente non ha ancora un metodo stabile, il modello viene interrogato in modo episodico, i criteri di qualita non sono espliciti e l'interazione dipende soprattutto dall'improvvisazione.

### Livello 2. Repeatable

Cominciano a emergere schemi riusabili. L'utente ripete certe strategie con il modello, riusa formati e artefatti, traduce le risposte del LLM in passaggi operativi, ma il processo resta ancora parzialmente opportunistico e poco formalizzato.

### Livello 3. Defined

La collaborazione e ormai strutturata. L'utente ha un workflow esplicito, suddivide il compito in sottotask, assegna al LLM ruoli diversi, mantiene una coerenza tra prompt, artefatti e output, e inizia a usare il modello come partner procedurale e non solo come fonte di idee.

### Livello 4. Managed

Il processo e gestito con metriche e controlli espliciti. L'utente monitora la qualita degli output, confronta strategie o modelli in modo sistematico, definisce criteri di validazione e introduce un controllo quantitativo del processo di collaborazione.

### Livello 5. Optimizing

La collaborazione umano-LLM e oggetto di miglioramento continuo. Il workflow viene raffinato sulla base di feedback, errori, confronti tra modelli e automazione progressiva; la coppia umano-LLM apprende come sistema.

## Corpus analizzato

La stima e basata sulle chat salienti gia estratte nel file:

- `2025-survey-analysis/phase1_salient_chats.md`

In particolare, il corpus minimo usato come base principale comprende:

- 2025-04-11, `gpt-4-5`, *Analisi questionari aperti*
- 2025-04-14, `gpt-4o`, *Analisi qualitativa vs quantitativa*
- 2025-04-15, `o1`, *New chat*
- 2025-04-16, `gpt-4-5`, *Analisi dati questionario artigianato*
- 2025-04-30, `gpt-4o`, *Unire file JSON risposte*
- 2025-04-30, `o3`, *Presentazione risultati ricerca*
- 2025-05-03, `o3`, *Creazione presentazione questionario studenti*
- 2025-05-03, `o3`, *Riorganizzazione categorie JSON*
- 2025-05-06, `o4-mini-high`, *Grafico a barre frequenze*

Come chat di confine sono state considerate anche le due del 7 maggio dedicate a variabili del campione, chi-quadro, sottogruppi e script.

## Evidenze osservate nelle chat

## 1. La fase iniziale parte chiaramente da una condizione di livello 1

Le prime conversazioni mostrano una situazione di forte esplorazione:

- l'utente chiede come si analizzano risposte aperte di un questionario;
- chiede se convenga usare categorie, punteggi, sentiment o altre tecniche;
- chiede la differenza tra analisi qualitativa e quantitativa;
- chiede se sulle domande aperte si possano fare analisi statistiche.

Questa parte e tipica del livello 1: il problema non e ancora strutturato e la collaborazione con il LLM serve prima di tutto a capire "che cosa bisogna fare".

## 2. Il LLM svolge una funzione di scaffolding metacognitivo, ma non ancora di vero Human-Under-Test

Nelle chat del 11 e 14 aprile il modello:

- chiarisce le differenze tra qualitativo e quantitativo;
- suggerisce coding, categorie, frequenze e sentiment;
- esplicita che per fare statistica sulle domande aperte occorre prima codificare il testo;
- propone una combinazione di tecniche, non una sola;
- aiuta a decomporre il problema in passaggi.

Questo corrisponde bene alle idee del paper su feedback, nudging e scaffolding. Tuttavia il modello non agisce ancora come un valutatore proattivo dell'umano nel senso forte di Casadei et al.: non interrompe, non testa sistematicamente la comprensione dell'utente, non verifica esplicitamente aspettative errate con micro-assessment mirati. Risponde bene, ma soprattutto in modo reattivo.

## 3. Tra meta aprile e inizio maggio emerge un uso ripetibile e orientato agli artefatti

Le chat successive mostrano una maturazione evidente:

- l'utente passa dal chiedere "come si fa" al chiedere output strutturati;
- compaiono tabelle con categorie, frequenze, risposte e sentiment;
- le categorie vengono trasformate in file JSON e poi riordinate o fuse;
- vengono effettuati controlli puntuali sulle frequenze di alcune categorie;
- il modello viene usato per strutturare slide, grafici e materiali per il gruppo di progetto.

Qui la collaborazione non e piu solo esplorativa. C'e gia una logica ripetibile:

1. definire il metodo;
2. applicarlo alle domande aperte;
3. trasformare i risultati in artefatti;
4. verificare e rifinire;
5. preparare la presentazione.

Questa e la caratteristica piu forte del livello 2.

## 4. Si intravede una transizione verso il livello 3

A fine prima fase la collaborazione diventa piu definita:

- vengono distinti sottocompiti diversi e assegnati a modelli differenti;
- il LLM non viene usato solo per spiegare, ma per produrre strutture, script, visualizzazioni e organizzazione del lavoro;
- l'utente dimostra crescente precisione nella richiesta, ad esempio su ordine delle colonne, aggregazione di categorie rare, output XLSX, gestione dei sottogruppi.

Questo mostra crescita della `User-AI Maturity` nel senso del paper: aumentano consapevolezza, adattivita e competenza strategica nel collaborare con l'AI. L'utente impara progressivamente come usare il modello non solo come "risponditore", ma come supporto procedurale e tecnico.

## 5. La consapevolezza statistica arriva, ma ancora come acquisizione emergente

Il terzo obiettivo che hai indicato e particolarmente importante: durante la prima fase maturi la consapevolezza che serva un'analisi statistica adeguata per confrontare sottogruppi per genere, anno e corso di studi.

Questa consapevolezza:

- non e pienamente presente all'inizio;
- emerge progressivamente grazie all'interazione;
- diventa esplicita il 7 maggio nelle chat su variabili del campione, chi-quadro e tabelle di contingenza.

Questo dato e cruciale per la stima: se la consapevolezza metodologica essenziale emerge solo alla fine della fase, allora la maturita della collaborazione non puo ancora essere considerata pienamente "managed" o "optimizing". La collaborazione sta maturando, ma non e ancora governata da un impianto metodologico quantitativo esplicito fin dall'inizio.

## 6. Non ci sono evidenze sufficienti per i livelli 4 e 5

Nel corpus della prima fase non si osservano ancora in modo stabile:

- metriche esplicite per valutare la qualita degli output del LLM;
- confronto sistematico tra modelli con criteri dichiarati;
- protocollo di validazione formalizzato delle categorie o dei grafici;
- strategia quantitativa completa e controllata per l'intero workflow;
- miglioramento continuo del processo sulla base di misure strutturate.

Per questo motivo non e difendibile assegnare il livello 4 o 5 alla prima fase.

## Stima finale

## Giudizio sintetico

Se devo assegnare **un solo livello** alla prima fase di collaborazione umano-LLM, la stima piu difendibile e:

**Livello 2 - Repeatable**, con una **transizione avanzata verso il Livello 3 - Defined**.

## Motivazione sintetica

La collaborazione:

- parte in modo chiaramente esplorativo e poco strutturato;
- sviluppa abbastanza presto pattern riusabili di interazione;
- produce artefatti coerenti e concatenati tra loro;
- mostra apprendimento del lato umano su come interrogare il modello e usare diversi modelli per scopi diversi;
- ma non raggiunge ancora un controllo metodologico pienamente esplicito, misurato e formalizzato.

## Stima dinamica lungo la timeline

Una formulazione ancora piu precisa e questa:

- **inizio della fase**: Livello 1 - Initial;
- **corpo centrale della fase**: Livello 2 - Repeatable;
- **fine della fase, intorno al 7 maggio 2025**: soglia tra Livello 2 e Livello 3.

## Lettura per dimensioni, coerente con il paper

### User Task Maturity

**Bassa all'inizio, media alla fine della fase.**

All'inizio manca una visione chiara del metodo di analisi del questionario. Alla fine emerge una migliore padronanza dei sottotask, ma non ancora una piena padronanza statistica.

### User-AI Maturity

**Media, con crescita evidente.**

L'utente mostra adattamento progressivo, affina le richieste, sfrutta diversi modelli in modo differenziato e usa il LLM per compiti via via piu mirati.

### AI Maturity nel supporto adattivo

**Media.**

Il LLM e utile nel guidare, strutturare e produrre output, ma nel corpus esaminato agisce soprattutto come assistente reattivo. Non emerge ancora una vera attivita proattiva di human testing nel senso forte del paper.

### Co-reasoning loop

**Presente ma ancora incompleto.**

Si osserva una co-evoluzione reale: il modello orienta il ragionamento dell'utente e l'utente migliora il modo in cui sfrutta il modello. Tuttavia il ciclo di riflessione reciproca non e ancora pienamente formalizzato.

## Formula breve riusabile nel paper

Una formulazione sintetica che puoi riusare nel testo e la seguente:

> L'analisi delle chat della prima fase suggerisce che la collaborazione tra il ricercatore e ChatGPT si collochi a un livello di maturity complessivamente pari a "Repeatable", con un chiaro avanzamento verso il livello "Defined" al termine della fase. L'interazione parte in forma esplorativa e ad hoc, ma evolve rapidamente in un workflow riusabile basato su decomposizione del compito, codifica delle risposte aperte, produzione di artefatti intermedi e supporto alla presentazione dei risultati. Rimangono pero assenti, in questa fase, elementi tipici dei livelli superiori, come una validazione sistematica degli output, metriche esplicite di qualita e un controllo quantitativo stabile dell'intero processo di collaborazione umano-LLM.

## Limiti della stima

- La stima e basata sulle chat salienti, non sull'intero archivio completo di tutte le conversazioni.
- Il paper di Casadei, Delnevo e Mirri e concettuale e non offre una scala operativa gia validata per questo specifico tipo di rating.
- Non sono stati ancora integrati, in questa stima, i materiali finali prodotti nella fase 1, come le slide definitive o il report finale consegnato.

## Possibile passo successivo

Il passo successivo piu utile sarebbe trasformare questa stima in una **rubrica analitica** con indicatori, ad esempio:

- calibration of expectations;
- decomposition of task;
- prompting strategy;
- evidence of verification;
- model differentiation;
- emergence of statistical awareness;
- autonomy vs dependence;
- continuity of feedback loop.

Questo permetterebbe una valutazione piu trasparente e piu facilmente difendibile in sede di paper.
