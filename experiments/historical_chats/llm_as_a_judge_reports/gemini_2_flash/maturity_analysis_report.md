# Report di Analisi della Maturità dell'Interazione Umano-LLM
## Progetto: Analisi del Questionario "CraftTrainer"

### 1. Introduzione
Il presente report valuta il livello di **Maturity** (Maturità) nella collaborazione tra l'utente (umano) e il Large Language Model (LLM) durante il processo di analisi di un questionario somministrato a studenti degli istituti tecnici e professionali del settore calzaturiero. L'analisi si basa sulla metodologia "LLM-as-a-judge", applicando il modello di maturità descritto da **Casadei, Delnevo e Mirri**, il quale si ispira al classico **Capability Maturity Model (CMM)** di **W. S. Humphrey (1989)**.

### 2. Modello di Riferimento
Il modello CMM di Humphrey prevede 5 livelli evolutivi:
1.  **Initial (Iniziale):** Processo ad hoc, spesso caotico e poco strutturato.
2.  **Repeatable (Ripetibile):** Vengono stabiliti processi di base per tracciare risultati e successi.
3.  **Defined (Definito):** Il processo è documentato, standardizzato e integrato in una metodologia chiara.
4.  **Managed (Gestito):** Il processo è monitorato e misurato attraverso metriche quantitative.
5.  **Optimizing (Ottimizzante):** Miglioramento continuo del processo attraverso feedback quantitativo e innovazione.

### 3. Analisi delle Interazioni (Chat Log)

L'evoluzione della collaborazione è stata suddivisa in cinque fasi salienti estratte dai log:

#### Fase 1: Esplorazione Metodologica (Livello 1 - Initial)
*Riferimento: Chat 1.1, 1.2*
L'umano inizia con domande di ampio respiro per comprendere come approcciare l'analisi di dati qualitativi e quantitativi. La conoscenza degli strumenti statistici e delle potenzialità dell'LLM è ancora in fase embrionale ("procedere a macchia d'olio"). L'LLM funge da tutor metodologico, spiegando la differenza tra i vari tipi di analisi.

#### Fase 2: Sperimentazione e Prima Applicazione (Livello 2 - Repeatable)
*Riferimento: Chat 1.3*
L'umano applica i primi concetti: fornisce una lista di risposte aperte e chiede una categorizzazione strutturata (Frequenza, Sentiment, Categorie). Viene stabilito un primo schema di output ripetibile per le diverse domande del questionario.

#### Fase 3: Sistematizzazione e Grounding Scientifico (Livello 3 - Defined)
*Riferimento: Chat 1.4, 2.1*
L'interazione si evolve verso un approccio più rigoroso. L'umano fornisce paper accademici per "ancorare" l'analisi a metodologie consolidate. Inizia la gestione sistematica dei dati (fusione di file JSON gerarchici), dimostrando una pianificazione del workflow più matura e definita.

#### Fase 4: Validazione, Controllo e Integrazione Professionale (Livello 4 - Managed)
*Riferimento: Chat 2.2, 2.3, 3.1, 3.2*
L'umano non accetta passivamente l'output dell'LLM ma lo **misura** e lo **valida** (check sui conteggi, confronto con grafici preesistenti). La collaborazione si sposta sulla produzione di output professionali di alto livello: codice LaTeX per un paper e presentazioni PowerPoint basate su template istituzionali (UNIBO). L'umano gestisce attivamente il "Prompt Engineering" per ottenere risultati conformi a standard specifici.

#### Fase 5: Ottimizzazione e Rigore Statistico (Livello 5 - Optimizing)
*Riferimento: Chat 3.3 - 4.2*
Nella fase finale, l'umano richiede analisi statistiche avanzate (Test $\chi^2$ di indipendenza) per valutare differenze significative tra sottogruppi (genere, corso, anno). Viene effettuato il debug del codice Python dell'LLM e viene richiesta l'uniformità dei report. L'umano dimostra di aver interiorizzato la metodologia, ottimizzando continuamente gli script e cercando una comprensione profonda dei test statistici applicati.

### 4. Valutazione Finale
Il livello di maturità raggiunto al termine della prima fase di analisi è stimabile come:
**LIVELLO 4/5 (Managed/Optimizing)**

L'utente è passato da un approccio esplorativo e incerto a una gestione magistrale della collaborazione con l'LLM, utilizzandolo come un "assistente ricercatore" capace di eseguire analisi complesse sotto una supervisione critica e metodologica costante.

### 5. Conclusioni e Raccomandazioni
La transizione verso la fase statistica successiva è supportata da una solida consapevolezza metodologica. Per il futuro si raccomanda di:
- Continuare l'integrazione di test statistici inferenziali (non solo descrittivi).
- Formalizzare la griglia di codifica qualitativa definitiva (Codebook) per garantire la replicabilità totale.
- Utilizzare l'LLM per la scrittura critica delle sezioni di "Discussione" e "Limitazioni" del paper, mantenendo l'approccio di validazione rigorosa osservato finora.

---
*Analisi eseguita secondo il metodo LLM-as-a-judge*
*Data: 14 Aprile 2026*
