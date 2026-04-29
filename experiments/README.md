# /experiments

Questa cartella raccoglie i materiali usati negli esperimenti e nelle analisi collegate.

## Struttura delle sotto-cartelle

- `new_chats/`: materiali relativi a nuove chat o replay dell'attivita sperimentale.
  - `dataset/`: dati e documentazione di supporto usati nelle nuove analisi.
    - `data/`: CSV contenente domande e risposte del questionario estratte da Google Form.
    - `docs/`: documenti contenenti le conversazioni tra umano e ChatGPT per analizzare il questionario.
    - `papers/`: paper e riferimenti bibliografici usati come supporto.
  - `llm_as_a_judge_reports/`: report di valutazione delle nuove chat generati da diversi modelli.
    - `gemini_2_Flash/`: report Gemini su maturity, problemi di interazione, completezza del contesto, valutazione proattivita LLM.
    - `gpt_5.4/`: report GPT-5.4 su maturity, problemi di interazione, completezza del contesto, valutazione proattivita LLM.
  - `prompts/`: prompt usati per eseguire le analisi (gli stessi usati per ogni modello).

- `historical_chats/`: materiali derivati da chat/interazioni storiche usate come base di analisi.
  - `llm_as_a_judge_reports/`: report prodotti con approccio "LLM as a judge" sulle chat storiche.
    - `gpt_5.4/`: valutazioni GPT-5.4 su contesto iniziale, maturity e problemi di interazione.
  - `salient_chats_for_step_1/`: estratti o passaggi di chat considerati piu rilevanti per il primo step.
  - `phase1_objectives.md`: elenco sugli obiettivi della prima fase (English).

