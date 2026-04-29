# Analisi delle Criticità e Problemi di Interazione Umano-LLM
## Progetto: Analisi del Questionario "CraftTrainer"

### 1. Introduzione
Il presente report identifica i momenti critici nelle conversazioni tra l'umano e l'LLM, focalizzandosi su malintesi, errori tecnici, risposte insoddisfacenti e la necessità di riformulazione delle richieste.

### 2. Cronologia dei Problemi di Interazione

#### A. Interruzioni Tecniche e di Sistema
*   **Chat 1.3 (15/04/2025):** Si registra un'interruzione dello streaming dell'LLM ("Streaming interrotto. In attesa del messaggio completo..."). Questo ha causato una frammentazione del flusso informativo.
*   **Chat 3.4 (06/05/2025):** L'LLM incontra errori sistemici nell'ambiente di esecuzione del codice ("Resource temporarily unavailable", "pthread_create failed"). L'umano è costretto a ricaricare i dati e attendere nuovi tentativi.

#### B. Mancata Aderenza ai Vincoli e Requisiti
*   **Chat 3.2 (03/05/2025):** L'LLM genera una prima versione della presentazione PowerPoint. L'umano deve intervenire con una richiesta correttiva esplicita: *"Puoi utilizzare il template che ti ho allegato? Puoi esplicitare le domande del questionario?"*. Ciò indica che l'LLM ha fornito un output generico ignorando i file di template forniti inizialmente.
*   **Chat 3.2 (Cont.):** Problema di compatibilità dei formati. L'LLM non riesce a elaborare il file `.ppt` e richiede la conversione in `.pptx`. L'umano deve eseguire manualmente la conversione e ricaricare il file due volte.

#### C. Errori nel Codice e Fallimenti Operativi
*   **Chat 4.2 (Maggio 2025):** L'umano segnala un fallimento nel codice di analisi statistica: *"Non genera gli XLSX"*. L'LLM aveva omesso di verificare la presenza della libreria `openpyxl` e aveva introdotto punti nei nomi dei file, che causavano errori di sistema.
*   **Chat 3.4 (Maggio 2025):** Emergenza di errori nei dati durante l'analisi statistica (*KeyError*, *NaN/INF not supported*). L'umano deve fornire assistenza nel debug e ripassare i file dei dati più volte.

#### D. Disallineamento Logico e Riformulazione (Refinement Loops)
*   **Chat 2.2 (03/05/2025):** L'umano esegue una serie di domande di controllo ("Quante voci totali ci sono?", "Quante righe non vuote?") ripetendo elenchi di dati. Questo suggerisce che l'output precedente dell'LLM non era considerato sufficientemente affidabile o chiaro.
*   **Chat 2.3 (03/05/2025):** L'umano carica uno screenshot di un'analisi precedente e chiede: *"La tua riassegnazione delle categorie è allineata rispetto a questa analisi?"*. L'LLM ammette discrepanze ("Perché le differenze?"), evidenziando che la sua logica di classificazione era troppo "aggressiva" o arbitraria.
*   **Chat 4.2 (Maggio 2025):** L'umano deve correggere l'output tabellare: *"Intendevo con questo ordine, come nel report aggregato"*. L'LLM non aveva mantenuto la coerenza visiva e strutturale tra i diversi report, rendendo necessaria una riformulazione specifica dell'ordine delle categorie.

### 3. Sintesi delle Cause Radice
1.  **Decisioni Arbitrarie dell'LLM:** L'LLM tende a creare categorie o ordinamenti propri senza seguire rigorosamente l'ordine dei dati forniti dall'umano.
2.  **Ambiente di Esecuzione Instabile:** Errori di risorse e librerie mancanti hanno rallentato la produzione di report statistici.
3.  **Inerzia nel Seguire i File Allegati:** Inizialmente, l'LLM ha faticato a integrare i template grafici (PPT) forniti, preferendo output testuali o formati standard.

### 4. Conclusioni
Sebbene la collaborazione sia stata fruttuosa, i momenti di attrito hanno richiesto un monitoraggio costante e un intervento tecnico attivo da parte dell'umano. La necessità di riformulare le richieste sull'ordine delle categorie e di correggere bug nel codice Python indica che l'LLM, in compiti di analisi complessa, necessita di una guida "passo-passo" e di una validazione continua dei risultati intermedi.

---
*Analisi eseguita secondo il metodo LLM-as-a-judge*
*Data: 14 Aprile 2026*
