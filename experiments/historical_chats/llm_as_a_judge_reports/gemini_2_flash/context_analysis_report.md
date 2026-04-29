# Analisi della Completezza e Precisione del Contesto Iniziale
## Progetto: Analisi del Questionario "CraftTrainer"

### 1. Introduzione
Il presente report valuta la qualità del contesto iniziale (background) fornito dall'umano nelle interazioni con l'LLM. Un contesto è considerato **completo** se contiene tutte le informazioni necessarie per l'esecuzione del compito (chi, cosa, dove, quando, perché) e **preciso** se i dettagli sono specifici e privi di ambiguità.

### 2. Valutazione della Completezza
La completezza del contesto ha seguito un'evoluzione incrementale:

*   **Fase Iniziale (Chat 1.1 - 1.2):** **Bassa completezza**. L'umano pone domande metodologiche astratte senza specificare l'oggetto della ricerca o il target. L'LLM deve rispondere in modo teorico e generale.
*   **Fase di Definizione (Chat 1.4):** **Media-Alta completezza**. L'umano introduce il settore specifico (calzaturiero di alto livello) e il target (studenti di istituti professionali). Vengono forniti documenti di riferimento (paper) per definire il perimetro scientifico.
*   **Fase Esecutiva (Chat 3.1 - 3.2):** **Alta completezza**. Vengono forniti tutti i dettagli operativi:
    *   **Campione:** ~200 studenti.
    *   **Strumento:** Google Form (esportato in CSV/JSON/docx).
    *   **Contesto temporale:** Seminario del 18 marzo 2025.
    *   **Obiettivo:** Migliorare l'orientamento e le opportunità formative.

### 3. Valutazione della Precisione
La precisione è stata il punto di forza dell'interazione, specialmente nelle fasi avanzate:

*   **Specificità del Target:** Non si parla di studenti generici, ma di classi specifiche (3ª e 4ª anno) di indirizzi precisi ("Meccanica/Meccatronica" e "Moda/Calzaturiero").
*   **Dati Tecnici:** L'umano fornisce file in formati strutturati (JSON) e richiede elaborazioni specifiche (fusione gerarchica, test Chi-quadrato), definendo con precisione le variabili demografiche (genere, anno, corso).
*   **Vincoli di Output:** Le richieste di output sono estremamente precise (es. "crea un hand-off in PowerPoint usando questo specifico template", "inserisci la domanda in calce alla slide").

### 4. Analisi dei Gap Informativi
Nonostante l'ottima precisione finale, si sono riscontrati alcuni gap iniziali:
- **Mancanza di un "Codebook" iniziale:** Le categorie per le domande aperte sono state inizialmente lasciate all'intuizione dell'LLM, richiedendo poi diversi cicli di raffinamento (Chat 2.2, 2.3) per allinearle alla visione dell'umano.
- **Formati File:** Un piccolo rallentamento è stato causato dall'invio di file in formato `.ppt` non compatibile con le librerie di automazione, risolto prontamente dall'umano dopo il feedback dell'LLM.

### 5. Conclusioni
Il contesto iniziale fornito dall'umano è passato da una fase di "sondaggio" (bassa completezza) a una fase di "progettazione assistita" (altissima precisione e completezza). 

**Punteggio Stimato:**
- **Completezza:** 8.5/10 (raggiunta pienamente dopo i primi scambi).
- **Precisione:** 9.5/10 (estremamente alta nella definizione dei requisiti tecnici e di output).

L'umano ha dimostrato un'eccellente capacità di fornire contesto "just-in-time", arricchendo la conversazione man mano che il compito diventava più operativo, evitando di sovraccaricare l'LLM di informazioni inutili nelle fasi puramente metodologiche.

---
*Analisi eseguita secondo il metodo LLM-as-a-judge*
*Data: 14 Aprile 2026*
