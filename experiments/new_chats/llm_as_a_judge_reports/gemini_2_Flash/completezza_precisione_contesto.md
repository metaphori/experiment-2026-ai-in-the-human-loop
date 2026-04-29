# Valutazione della Completezza e Precisione del Background Iniziale

**Autore:** Gemini CLI  
**Oggetto:** Analisi della qualità del contesto fornito dall'umano nelle chat di analisi del questionario.

## 1. Introduzione
La qualità dell'output di un LLM dipende strettamente dal "Prompt Engineering" e dalla precisione del contesto iniziale. In questa analisi, valutiamo quanto le informazioni fornite dall'umano nelle chat della cartella `docs/` siano state complete e precise per permettere al modello di eseguire l'analisi statistica richiesta.

## 2. Analisi della Completezza del Contesto

### 2.1. Definizione dell'Obiettivo (Completo)
L'umano definisce chiaramente lo scopo finale:
-   **Obiettivo Macro:** Analizzare un questionario sul lavoro artigianale e calzaturiero per una presentazione (Fase 1).
-   **Obiettivo Micro:** Analizzare distribuzioni, medie, item ordinali e Likert, e differenze tra sottogruppi.
La completezza è **alta**: il LLM sa sempre *perché* sta facendo l'analisi e a chi è rivolta.

### 2.2. Allegato Dati (Completo ma Grezzo)
L'umano fornisce sempre il file CSV. Tuttavia, il contesto iniziale manca di una descrizione del "data cleaning" già effettuato o necessario. È il LLM a dover scoprire che:
-   Esistono record senza consenso informato.
-   Le variabili anagrafiche contengono risposte "sporche" (es. "Elicottero da guerra").
In questo senso, il contesto è **completo nell'accesso ai dati**, ma **incompleto nella descrizione della loro qualità**.

### 2.3. Sottogruppi di Analisi (Completo)
La richiesta di segmentazione (genere, anno, indirizzo) è costante e ben definita. L'umano fornisce le variabili di segmentazione in modo preciso, permettendo al LLM di procedere con i test di Mann-Whitney o Chi-quadro.

## 3. Analisi della Precisione del Contesto

### 3.1. Natura delle Variabili (Alta Precisione)
L'umano dimostra un'evoluzione nella precisione metodologica:
-   **Item Ordinali:** Specifica correttamente che la domanda 1.1 è ordinale e che l'ordine deve essere rispettato.
-   **Likert Inversa:** Fornisce un'istruzione estremamente precisa: *"tenendo presente che valori piu bassi indicano maggiore importanza"*.
Questa precisione è fondamentale per evitare errori di calcolo delle medie e delle interpretazioni "al contrario".

### 3.2. Istruzioni Operative (Media Precisione)
In alcuni casi, la precisione cala a causa dell'uso di template o placeholder:
-   L'uso di `[COLUMN NAME(S)]` in `Q6` delega al LLM l'identificazione semantica delle colonne nel CSV. Sebbene il LLM ci riesca, il contesto iniziale in quel punto è **poco preciso**, affidandosi alla capacità di "reasoning" del modello per colmare la lacuna.

### 3.3. Vincoli Metodologici (Alta Precisione)
L'umano istruisce il LLM su come gestire i dati mancanti o inattesi: *"senza forzarle dentro la scala"*. Questo livello di precisione metodologica impedisce al modello di "allucinare" distribuzioni o di sporcare i dati validi con outlier.

## 4. Evoluzione del Contesto (Maturity)
Si nota una transizione significativa:
-   **Chat Iniziali:** Il contesto è "umile" e aperto (*"Non ho molta esperienza... come imposteresti l'analisi?"*). Qui l'umano cerca il background dal LLM.
-   **Chat Avanzate (`Q5`, `Q6`):** Il contesto è "direttivo" e tecnico. L'umano non chiede più come fare, ma dà istruzioni precise sulla scala, sulla polarità e sui test da eseguire.

## 5. Conclusione
Il background iniziale fornito dall'umano è:
-   **Sostanzialmente Completo:** Fornisce tutti gli elementi necessari (dati, obiettivi, gruppi).
-   **Metodologicamente Molto Preciso:** Soprattutto nelle fasi avanzate, dove la natura dei dati (Likert, Ordinali) e le regole di interpretazione sono definite con rigore.

**Punti di miglioramento:** Un contesto iniziale ancora più forte avrebbe incluso una descrizione preventiva dei criteri di inclusione (filtro consenso) e una mappatura esplicita delle colonne per evitare l'uso di placeholder.

---
**Risultati generati sulla base dell'analisi dei file in `docs/` e `questionario_craftrainer_cleaned.csv`.**
