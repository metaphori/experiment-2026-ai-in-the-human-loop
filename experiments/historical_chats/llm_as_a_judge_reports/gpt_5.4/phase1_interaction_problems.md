[phase1_initial_context_quality.md](../../../experiment-2026-haic-extension-local/2025-survey-analysis/phase1_initial_context_quality.md)# Problemi di interazione nelle chat della prima fase di analisi del questionario

## Perimetro

Analisi limitata alla prima fase del lavoro sul questionario, cioe alle chat fino al **7 maggio 2025**, data della prima presentazione al gruppo di ricerca.

Fonte principale:
- `2025-survey-analysis/CT_Survey_2025_GPT_chats.xlsx`

## Criterio usato

Ho considerato come segnali di problema di interazione i punti della cronologia in cui:

- l'utente ripete o riformula una richiesta molto simile nella stessa chat;
- l'utente segnala esplicitamente che l'output non funziona;
- l'utente restringe o corregge il requisito subito dopo una risposta del modello;
- l'utente chiede un chiarimento concettuale che suggerisce che la risposta precedente non era sufficientemente interpretabile o operativa.

Non tutti questi casi indicano un "errore grave" del LLM. Alcuni mostrano soprattutto:

- ambiguita iniziale della richiesta;
- mismatch tra formato dell'output e bisogno reale dell'utente;
- difficolta dell'LLM nel soddisfare vincoli grafici o di esecuzione locale;
- mancanza di scaffolding concettuale sufficiente per usare davvero l'output.

## Momenti in cui emergono problemi di interazione

## 1. Ambiguita sull'unita di conteggio

### 2025-05-03T13:46:42+02:00 | gpt-4o | `Voci con Manualità JSON`

Turno utente:
- "Quante frasi non vuote ci sono in questo elenco (considera intere anche quelle che vanno a capo)"

Perche e un segnale di problema:
- pochi secondi prima l'utente aveva chiesto quante "righe non vuote" ci fossero;
- il passaggio da "righe" a "frasi" mostra che la prima formulazione non rappresentava il bisogno reale;
- non e necessariamente un fallimento del modello, ma un caso di **task framing incompleto** che costringe l'utente a riformulare.

Tipo di problema:
- ambiguita del compito;
- riformulazione dell'unita di analisi.

## 2. Richiesta di grafico ripetuta dopo una prima risposta non soddisfacente

### 2025-05-05T19:22:21+02:00 | o4-mini | `Grafico barre orizzontale`

Turno utente:
- ripete sostanzialmente la stessa richiesta iniziale di generare un grafico a barre orizzontali aggregando le frequenze uguali a 1 in "Altro".

Perche e un segnale di problema:
- nella stessa chat il modello aveva gia risposto con snippet Python e con un "grafico finto" descritto testualmente;
- la ripetizione quasi identica della richiesta suggerisce che l'output precedente non fosse percepito come sufficiente rispetto al bisogno di ottenere un grafico davvero utilizzabile.

Tipo di problema:
- output non allineato al formato atteso;
- richiesta ripetuta.

## 3. Fallimento operativo del codice suggerito

### 2025-05-05T19:23:32+02:00 | o4-mini | `Grafico barre orizzontale`

Turno utente:
- "ottengo questo errore: ... AttributeError: 'FigureCanvasInterAgg' object has no attribute 'tostring_rgb' ..."

Perche e un segnale di problema:
- e il caso piu esplicito di attrito nella chat;
- il codice fornito dal modello non e eseguibile senza problemi nell'ambiente locale dell'utente;
- l'interazione deve spostarsi dalla generazione del grafico al debugging dell'ambiente.

Tipo di problema:
- incompatibilita ambiente-codice;
- fallimento operativo esplicito.

## 4. La stessa richiesta di grafico riappare il giorno successivo

### 2025-05-06T08:08:01+02:00 | o4-mini-high | `Grafico a barre frequenze`

Turno utente:
- "Puoi generarmi un grafico a barre a partire da quello viola, aggregando le frequenze = 1 in 'Altro' e creandone uno con frequenze e percentuali come quello a barre nere allegato?"

Perche e un segnale di problema:
- e una sostanziale reiterazione del bisogno del giorno prima;
- la richiesta riemerge dopo che la chat precedente aveva incontrato problemi tecnici e non aveva portato a un risultato pienamente soddisfacente;
- segnala una **ripresa del task** dovuta a soluzione incompleta.

Tipo di problema:
- richiesta reiterata dopo esito insoddisfacente;
- continuita debole tra soluzione proposta e risultato ottenuto.

## 5. L'output grafico ottenuto non e ancora usabile come desiderato

### 2025-05-06T08:18:56+02:00 | o4-mini-high | `Grafico a barre frequenze`

Turno utente:
- invia il grafico ottenuto e chiede: "Come si fa a modificare questo grafico in modo che il valore percentuale stia all'interno del riquadro?"

Perche e un segnale di problema:
- dopo che il modello aveva dichiarato di aver generato il grafico, l'utente mostra che il layout non e ancora adeguato;
- il problema qui non e il dato, ma l'**usabilita visiva** dell'output.

Tipo di problema:
- mismatch tra output prodotto e requisito grafico effettivo;
- necessita di correzione post hoc.

## 6. Riformulazione immediata del vincolo grafico

### 2025-05-06T08:21:51+02:00 | o4-mini-high | `Grafico a barre frequenze`

Turno utente:
- "C'è modo di mostrare frequenza e percentuale fuori dalle barre, a destra delle barre stesse, in modo che sia più leggibile, pur stando dentro al riquadro?"

Perche e un segnale di problema:
- pochi minuti prima l'utente aveva chiesto di far stare l'etichetta "all'interno del riquadro";
- dopo la risposta del modello, il requisito viene precisato in modo piu vincolato: non dentro la barra, ma fuori dalla barra e comunque dentro il riquadro del grafico;
- questo mostra un **allineamento ancora incompleto** tra la soluzione suggerita e l'esigenza visuale reale.

Tipo di problema:
- riformulazione del requisito;
- chiarimento successivo a risposta parzialmente adeguata.

## 7. Prima correzione di dettaglio sullo script statistico

### 2025-05-07T11:51:51+02:00 | o4-mini-high | `Analisi statistica questionario`

Turno utente:
- "Puoi fare in modo che 'non specificato' e 'altro' vengano messi nelle ultime due colonne in tutte le analisi?"

Perche e un segnale di problema:
- il modello aveva appena proposto una prima versione dello script;
- l'utente e costretto a intervenire subito per correggere un requisito di ordinamento non soddisfatto;
- non e un fallimento grave, ma indica che l'output iniziale non copriva ancora tutti i vincoli pratici richiesti.

Tipo di problema:
- incompleta soddisfazione dei requisiti;
- raffinamento necessario immediato.

## 8. Specifiche aggiuntive emerse solo dopo la seconda versione

### 2025-05-07T11:56:27+02:00 | o4-mini-high | `Analisi statistica questionario`

Turno utente:
- aggiunge percorso del JSON, cartella `reports/numero_domanda`, generazione di file XLSX e file riepilogativo multi-sheet.

Perche e un segnale di problema:
- il bisogno operativo reale si esplicita solo dopo la seconda risposta;
- questo puo dipendere sia da evoluzione naturale del compito sia da una risposta ancora troppo generica del modello rispetto all'uso pratico;
- e un caso intermedio tra normale iterazione e interazione non pienamente risolta.

Tipo di problema:
- specifica tardiva dei requisiti;
- output iniziale non ancora abbastanza operativo.

## 9. Il modello fornisce uno script che non produce gli XLSX attesi

### 2025-05-07T12:02:05+02:00 | o4-mini-high | `Analisi statistica questionario`

Turno utente:
- "Non genera gli XLSX: ..."

Perche e un segnale di problema:
- questo e il secondo caso piu netto di fallimento esplicito, dopo l'errore del grafico;
- il modello aveva promesso l'esportazione dei file Excel, ma l'utente deve segnalare che il risultato non si verifica;
- l'interazione passa da generazione di codice a **debugging di una promessa non mantenuta**.

Tipo di problema:
- fallimento operativo esplicito;
- mismatch tra output dichiarato e output reale.

## 10. Chiarimento concettuale necessario per capire il test statistico

### 2025-05-07T12:06:22+02:00 | o4-mini-high | `Analisi statistica questionario`

Turno utente:
- "Puoi esplicitare meglio cosa confronti con il test chi-quadro?"

Perche e un segnale di problema:
- anche dopo avere ricevuto lo script, l'utente non ha ancora un modello mentale abbastanza chiaro di cosa il test stia confrontando;
- il problema non e piu tecnico, ma di **trasparenza esplicativa**;
- questo indica che la risposta del LLM era operativa ma non abbastanza interpretativa.

Tipo di problema:
- insufficiente scaffolding concettuale;
- bisogno di spiegazione metodologica.

## 11. L'utente chiede di esplicitare i valori confrontati nella tabella finale

### 2025-05-07T12:06:52+02:00 | o4-mini-high | `Analisi statistica questionario`

Turno utente:
- "Anche nella tabella di analisi chi-quadro sarebbe utile avere le colonne relative ai valori confrontati"

Perche e un segnale di problema:
- subito dopo il chiarimento sul chi-quadro, emerge un ulteriore limite dell'output;
- non basta sapere in astratto cosa confronta il test: l'utente ha bisogno che il confronto sia reso leggibile anche nell'artefatto finale;
- questo mostra una **frizione tra correttezza statistica e leggibilita dell'output**.

Tipo di problema:
- insufficiente leggibilita del risultato;
- richiesta di rendere l'output autoesplicativo.

## Sintesi interpretativa

I problemi di interazione emersi nella prima fase si concentrano soprattutto in due aree:

1. **Produzione di artefatti eseguibili o visivi**
   - grafici non immediatamente riusabili;
   - codice che non gira nell'ambiente locale;
   - necessita di molte correzioni di layout.

2. **Produzione di script e output statistici interpretabili**
   - script che non soddisfano subito tutti i requisiti pratici;
   - esportazioni promesse ma non funzionanti;
   - spiegazioni concettuali non sufficienti a rendere il test statistico davvero comprensibile e leggibile.

Nel complesso, i segnali piu forti di problema di interazione sono:

- `2025-05-05T19:22:21+02:00` richiesta di grafico ripetuta;
- `2025-05-05T19:23:32+02:00` errore esplicito del codice per il grafico;
- `2025-05-06T08:08:01+02:00` reiterazione della stessa esigenza grafica il giorno successivo;
- `2025-05-07T12:02:05+02:00` mancata generazione degli XLSX promessi;
- `2025-05-07T12:06:22+02:00` richiesta di chiarimento sul significato del chi-quadro.

## Nota finale

Ho escluso dai casi principali le semplici domande di approfondimento iniziale sulla metodologia, perche in quelle chat il passaggio da una domanda all'altra sembra fisiologico e non e accompagnato da segnali chiari di insoddisfazione. Ho escluso anche la chat `Presentazione risultati ricerca` come evidenza forte di problema, perche l'export mostra una traccia anomala o incompleta della risposta del modello, ma senza un follow-up dell'utente che permetta di interpretarla con affidabilita.
