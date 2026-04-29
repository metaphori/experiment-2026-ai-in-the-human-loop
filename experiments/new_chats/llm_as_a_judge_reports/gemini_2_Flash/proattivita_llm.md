# Analisi della Proattività dell'LLM nelle Interazioni di Ricerca (HAI-2)

Il presente documento analizza le interazioni tra l'umano e l'LLM documentate nella cartella `docs/`, focalizzandosi sui momenti in cui un approccio più proattivo da parte dell'LLM avrebbe potuto migliorare l'efficacia della collaborazione, la qualità dei dati o la fluidità del processo di analisi.

---

## 1. Pulizia e Audit dei Dati (Data Cleaning)

In diverse chat, l'LLM identifica correttamente problemi nei dati grezzi (risposte "troll" nel genere, anomalie nell'anno di corso, mancanza di consenso). Tuttavia, spesso si limita a segnalarli o a suggerire come l'utente dovrebbe gestirli, invece di proporre un'azione immediata o chiedere istruzioni specifiche per procedere.

*   **Momenti di mancata proattività:**
    *   **Gestione del Consenso:** L'LLM nota che 10 rispondenti non hanno dato il consenso (Consensus = No). Avrebbe potuto chiedere: *"Ho rilevato 10 casi senza consenso. Vuoi che li escluda permanentemente dal dataset prima di procedere con qualsiasi analisi?"*
    *   **Risposte Anomale (Outlier):** Identifica risposte come "Robot" o "Elicottero" nel genere. Invece di descriverle come "problemi", avrebbe potuto proporre una strategia di ricodifica: *"Ho trovato 5 risposte non valide nel campo Genere. Preferisci che le raggruppi in una categoria 'Altro/Non specificato' o che le escluda dalle analisi comparative?"*
    *   **Standardizzazione degli Indirizzi:** L'LLM rileva varianti come "moda e calzatura" e "Moda e calzatura". Avrebbe potuto offrire: *"Posso generare una tabella di mappatura per uniformare automaticamente i nomi degli indirizzi di studio. Vuoi che ti mostri una proposta di raggruppamento?"*

## 2. Definizione del Percorso Metodologico

L'LLM fornisce ottimi consigli metodologici (fasi dell'analisi, tipi di variabili), ma spesso attende che l'utente chieda "cosa fare" invece di guidare attivamente l'utente verso il passo successivo logico.

*   **Momenti di mancata proattività:**
    *   **Scelta degli Strumenti:** L'LLM suggerisce che alcune analisi sono meglio fatte in Python/Pandas. Avrebbe potuto dire: *"Dato che il file è un CSV, posso scrivere ed eseguire io stesso uno script per generare queste tabelle descrittive immediatamente. Procedo?"*
    *   **Approfondimento delle Domande Aperte:** Suggerisce la "codifica tematica". Avrebbe potuto essere proattivo offrendo un esempio: *"Per la domanda 1.2 (capacità necessarie), ho analizzato i primi 20 record e propongo queste 5 categorie. Ti sembrano adeguate per procedere con l'intero dataset?"*
    *   **Obiettivi di Ricerca:** L'LLM accetta il dataset "così com'è". Sarebbe stato utile chiedere: *"Qual è l'obiettivo principale di questa analisi? (es. tesi accademica, report aziendale, orientamento scolastico). Conoscere il target mi aiuterebbe a dare priorità a certe variabili rispetto ad altre."*

## 3. Gestione Tecnica e Struttura dei Dati

Il caso più evidente di criticità tecnica emerge nella gestione dei file JSON per le categorie delle domande aperte.

*   **Momenti di mancata proattività:**
    *   **Prevenzione dell'Errore sui Duplicati:** L'LLM accetta un formato JSON `{risposta: categoria}` che intrinsecamente perde dati in caso di risposte identiche (chiavi duplicate). Un LLM proattivo, conoscendo i limiti del formato JSON, avrebbe dovuto avvisare *prima*: *"Attenzione: se usi la risposta testuale come chiave nel JSON, perderemo i conteggi per le risposte identiche. Ti suggerisco di usare una lista di oggetti o di coppie."*
    *   **Automazione della Conversione:** Una volta rilevato l'errore, invece di limitarsi a spiegare perché il conteggio era sbagliato, avrebbe potuto offrire: *"Posso scrivere un piccolo tool per convertire i tuoi prossimi file JSON in un formato più sicuro prima di analizzarli."*

## 4. Narrazione e Presentazione dei Risultati

Quando l'utente chiede come preparare una presentazione rapida, l'LLM suggerisce una struttura, ma non si propone come "curatore" della narrazione.

*   **Momenti di mancata proattività:**
    *   **Sintesi Narrativa:** L'LLM analizza i grafici uno per uno. Avrebbe potuto proporre: *"Ho analizzato le prime 3 domande aperte. Emerge un pattern chiaro: gli studenti apprezzano la manualità ma temono la scarsa crescita economica. Vuoi che prepari una slide di sintesi che metta in relazione questi due aspetti?"*
    *   **Visualizzazione Dati:** L'LLM produce grafici standard. Avrebbe potuto chiedere: *"Per la presentazione, preferisci grafici minimalisti in bianco e nero o qualcosa di più colorato e adatto a una platea di studenti/aziende?"*

## Conclusione

L'LLM ha dimostrato un'eccellente capacità analitica "reattiva" (rispondendo bene alle domande dirette), ma è rimasto spesso un passo indietro rispetto al potenziale di un "collaboratore esperto". La proattività si sarebbe potuta manifestare maggiormente nel:
1.  **Anticipare i problemi tecnici** (formati dati).
2.  **Proporre azioni concrete** (script di pulizia, bozze di codebook) senza aspettare l'input dell'utente.
3.  **Contestualizzare l'analisi** chiedendo attivamente gli scopi della ricerca.
