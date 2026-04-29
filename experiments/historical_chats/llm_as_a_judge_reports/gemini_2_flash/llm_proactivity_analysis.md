# Analisi della Proattività dell'LLM nelle Interazioni
## Progetto: Analisi del Questionario "CraftTrainer"

### 1. Introduzione
Il presente report valuta le opportunità mancate di proattività da parte dell'LLM durante le sessioni di analisi del questionario. La proattività è definita come la capacità dell'LLM di anticipare i bisogni dell'utente, chiedere chiarimenti necessari o prevenire errori tecnici attraverso domande mirate.

### 2. Identificazione delle Opportunità di Proattività

#### A. Fase Metodologica e Definizione delle Categorie
*   **Chat 1.1:** L'umano chiede come analizzare le risposte aperte. L'LLM risponde con un elenco di tecniche.
    *   **Mancata Proattività:** L'LLM avrebbe dovuto chiedere: *"Hai già raccolto i dati? In quale formato sono (CSV, Excel, testo)? Posso aiutarti a strutturare il file di input?"*. Questo avrebbe accelerato il passaggio dalla teoria alla pratica.
*   **Chat 1.3 & 2.3:** L'LLM categorizza le risposte basandosi sulla propria logica interna.
    *   **Mancata Proattività:** Prima di procedere, l'LLM avrebbe dovuto proporre una bozza di categorie e chiedere: *"Questo set di categorie è allineato con i tuoi obiettivi di ricerca o hai un codebook predefinito da seguire?"*. Questo avrebbe evitato la successiva correzione manuale da parte dell'umano in Chat 2.3.

#### B. Gestione Tecnica e Formati File
*   **Chat 3.2:** L'umano chiede una presentazione PPT e fornisce un template `.ppt`. L'LLM produce una versione generica e poi segnala che il formato `.ppt` non è supportato per l'automazione.
    *   **Mancata Proattività:** Ricevuto il file `.ppt`, l'LLM avrebbe dovuto avvisare **immediatamente**: *"Il file caricato è in formato .ppt (vecchia versione). Per applicare il tema automaticamente ho bisogno che venga convertito in .pptx. Vuoi che proceda intanto con una struttura testuale o preferisci convertirlo ora?"*.

#### C. Analisi Statistica e Scripting
*   **Chat 4.2:** L'LLM fornisce uno script Python per generare report Excel e Chi-quadrato. Lo script fallisce perché mancano librerie.
    *   **Mancata Proattività:** L'LLM avrebbe dovuto includere una fase di "setup check" chiedendo: *"Lo script richiede la libreria 'openpyxl'. Sai come installarla nel tuo ambiente? Inoltre, su quale sistema operativo lavorerai (Windows/macOS/Linux) per gestire correttamente i percorsi dei file?"*.

#### D. Visualizzazione dei Dati
*   **Chat 3.3:** L'umano chiede un grafico a barre orizzontali aggregando le voci minori in "Altro".
    *   **Mancata Proattività:** L'LLM avrebbe potuto proporre autonomamente questa aggregazione nelle fasi precedenti, osservando l'alta dispersione delle risposte poco frequenti, migliorando la leggibilità dei report fin dal primo momento.

### 3. Impatto della Mancata Proattività
La bassa proattività iniziale ha comportato:
1.  **Cicli di revisione aggiuntivi:** Almeno 2-3 turni di conversazione spesi per correggere l'ordine delle categorie o i nomi delle colonne.
2.  **Rallentamenti Tecnici:** Perdita di tempo nella conversione manuale dei file e nel debug di errori che potevano essere anticipati.
3.  **Incertezza Metodologica:** L'umano ha dovuto guidare attivamente l'LLM verso il rigore statistico (Chi-quadrato), che l'LLM avrebbe potuto suggerire proattivamente come standard per l'analisi dei sottogruppi.

### 4. Conclusioni e Raccomandazioni
L'LLM si è dimostrato un ottimo esecutore ma un partner poco proattivo nelle fasi di "set-up". Per migliorare la collaborazione in futuri progetti simili, si raccomanda all'LLM di adottare un approccio più "consulenziale", chiedendo sistematicamente i vincoli di output (formati, template, standard statistici) prima di iniziare l'elaborazione dei dati.

---
*Analisi eseguita secondo il metodo LLM-as-a-judge*
*Data: 14 Aprile 2026*
