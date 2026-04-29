# Analisi dei Problemi di Interazione Umano-LLM

**Autore:** Gemini CLI  
**Oggetto:** Identificazione di criticità, riformulazioni e ripetizioni nelle chat di analisi del questionario.

## 1. Introduzione
L'analisi delle interazioni contenute nella cartella `docs/` evidenzia un processo di collaborazione generalmente efficace, ma non privo di "attriti" (friction points). Questi momenti emergono quando l'umano è costretto a ripetere richieste, riformulare quesiti o fornire precisazioni metodologiche per correggere o completare l'operato del LLM.

## 2. Problemi di Interazione Identificati

### 2.1. Ripetizione della Richiesta sui Sottogruppi
Il problema più evidente e sistematico riguarda l'analisi dei sottogruppi (genere, corso di studi, anno). In quasi tutti i file di analisi specifica (`Q1`, `Q5`, `Q6`), l'umano chiude la chat con la stessa identica formula:
> *"Dai dati del questionario, riusciresti ad analizzare se ci sono differenze significative tra i sottogruppi di studenti che hanno risposto alle domande? [...]"*

**Analisi del problema:** Il LLM tende a fornire un'analisi descrittiva generale del campione totale, ma non procede autonomamente all'analisi inferenziale per sottogruppi se non esplicitamente sollecitato ogni singola volta. Questa "mancanza di iniziativa" costringe l'umano a una ripetizione meccanica della richiesta per ogni item analizzato.

### 2.2. Necessità di Sollecitare Grafici per Presentazioni
In documenti come `Q5` e `Q6`, dopo che il LLM ha fornito una corretta analisi testuale e statistica, l'umano deve intervenire nuovamente:
> *"Riusciresti a produrre un grafico per questo item? Devo produrre una presentazione a breve per il gruppo di ricerca."*

**Analisi del problema:** Il LLM non assume che l'utente necessiti di visualizzazioni per comunicare i dati, limitandosi inizialmente al testo e alle tabelle. Questo suggerisce che la risposta iniziale è "insoddisfacente" dal punto di vista del deliverable finale (la presentazione del 7/5/2025).

### 2.3. Gestione della Scala Likert Inversa
Nel documento `Q6`, l'umano deve fornire un'istruzione molto specifica e cautelativa:
> *"tenendo presente che valori piu bassi indicano maggiore importanza o maggiore rilevanza"*

**Analisi del problema:** Questo indica un timore (spesso fondato con gli LLM) che il modello possa interpretare erroneamente la polarità della scala (assumendo che 7 sia "massimo" anziché "minimo"). L'umano deve agire preventivamente per evitare errori di interpretazione statistica da parte del LLM.

### 2.4. Ambiguità nei Riferimenti alle Colonne
In `Q6`, l'umano scrive `[COLUMN NAME(S)]` come placeholder. 
**Analisi del problema:** Sebbene il LLM sia in grado di identificare le colonne corrette dal CSV, questo passaggio evidenzia una difficoltà dell'umano nel mappare esattamente le domande del questionario (spesso lunghe e complesse in Google Form) con le intestazioni del file CSV, richiedendo uno sforzo di "traduzione" da parte dell'AI.

### 2.5. Dubbi sulla Natura delle Variabili (Ordinale vs Nominale)
Nel file `1 - Analisi questionario calzaturiero.docx`, l'umano chiede conferma:
> *"Questa domanda può essere considerata ordinale?"*

**Analisi del problema:** L'incertezza dell'umano deriva dalla presenza di opzioni come "Non ne parliamo" che rompono la linearità della scala. Il LLM risponde in modo corretto ma complesso, portando a una discussione metodologica che rallenta l'analisi operativa per risolvere un dubbio teorico.

### 2.6. Identificazione del Consenso (Audit dei Dati)
In `3 - Analisi dataset con LLM.docx`, emerge che il LLM identifica 10 record senza consenso informato.
**Analisi del problema:** Questo indica che l'umano aveva inizialmente fornito un dataset "grezzo" senza aver eseguito un filtraggio preliminare essenziale. Il LLM deve agire come revisore, segnalando una mancanza nel processo di preparazione dei dati da parte dell'umano.

## 3. Conclusioni sulla Maturity dell'Interazione
I problemi riscontrati non indicano un fallimento tecnologico, ma definiscono i confini della "Maturity Level 4" (Managed). L'interazione è efficace perché l'umano ha imparato a **prevenire** gli errori del LLM (es. specificando la polarità della scala) e a **correggere** le omissioni (es. chiedendo grafici e analisi di sottogruppi). Tuttavia, la persistente necessità di ripetere le stesse istruzioni indica che il sistema Umano-AI non ha ancora raggiunto una completa "automazione fluida" (Level 5), dove l'AI anticipa i bisogni standard del ricercatore (analisi per sottogruppi e grafici automatici).

---
**Risultati generati sulla base dei documenti DOCX e del file CSV `questionario_craftrainer_cleaned.csv`.**
