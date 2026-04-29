# Problemi di interazione emersi nelle chat ChatGPT sull'analisi del questionario

## Obiettivo

Questo report identifica i momenti della cronologia delle chat in `docs` in cui emergono problemi di interazione tra umano e LLM. Per "problema di interazione" intendo un punto del dialogo in cui si osserva almeno uno di questi segnali:

1. l'umano deve ripetere, riformulare o restringere la richiesta per ottenere cio che gli serve davvero
2. l'umano deve correggere o far ricontrollare un output del LLM
3. il LLM segnala di non avere accesso al contesto o all'allegato che il turno umano dava per disponibile
4. la soluzione proposta dal LLM risolve il caso locale ma non il bisogno pratico che l'umano aveva in mente

Nel report uso la notazione `Hn/Ln` per indicare, dentro ciascun documento, il turno umano e il turno LLM corrispondente.

## Corpus analizzato

Sono stati esaminati 11 file `.docx` nella cartella `docs`.

I casi sotto sono divisi in:

- problemi di interazione ad alta confidenza
- segnali di attrito a confidenza media
- anomalie documentali da tenere separate dai veri problemi di interazione

## Problemi di interazione ad alta confidenza

| ID | Documento e istante | Tipo di problema | Evidenza sintetica | Perche e un problema di interazione | Gravita |
| --- | --- | --- | --- | --- | --- |
| P1 | `4 - Analisi preliminare questionario.docx`, `H2 -> L2` | Handoff fallito dell'allegato | l'umano dice di allegare un JSON di esempio; il LLM risponde che vede solo il CSV e chiede di allegare di nuovo il file | il contesto che l'umano ritiene gia disponibile non arriva al LLM; la collaborazione si interrompe finche l'umano non reinvia il materiale | Media |
| P2 | `4 - Analisi preliminare questionario.docx`, `H3 -> L3 -> H4 -> L4` | Errore di parsing/conteggio | il LLM conta `122` risposte categorizzate; l'umano obietta che nel JSON vede `137` righe e chiede di ricontrollare; il LLM ammette che il JSON piatto sovrascriveva chiavi duplicate | e il caso piu netto di output insoddisfacente corretto solo dopo una verifica esplicita dell'umano | Alta |
| P3 | `4 - Analisi preliminare questionario.docx`, `H5 -> L5` | Soluzione non allineata al bisogno operativo | dopo il caso singolo corretto, l'umano chiede uno script Python per gestire tutte le domande aperte | segnala che la risposta precedente era utile per un esempio, ma non ancora nel formato di lavoro realmente comodo e scalabile per l'utente | Media |

## Segnali di attrito a confidenza media

| ID | Documento e istante | Tipo di attrito | Evidenza sintetica | Lettura interpretativa | Gravita |
| --- | --- | --- | --- | --- | --- |
| A1 | `3 - Analisi dataset con LLM.docx`, `H2` dopo `L1` | Risposta iniziale troppo generale rispetto al bisogno operativo | dopo una lunga risposta su come usare gli LLM, l'umano restringe subito il focus a: "una domanda alla volta sarebbe piu preciso, anche statisticamente?" | non e una correzione esplicita, ma un chiaro bisogno di trasformare una risposta metodologica ampia in una regola pratica d'uso | Bassa-Media |
| A2 | `Q1 (OT) - 2.3 - Analisi risposte calzaturiero.docx`, `H2 -> L2` e `H3 -> L3` | Disallineamento di schema tra coding del LLM e coding dell'umano | il LLM produce una codifica sintetica a 5 categorie; l'umano poi usa un proprio file `r2.3.json` con 8 categorie e chiede confronti e sottogruppi su quello schema | la conversazione mostra che la prima codifica del LLM non era direttamente commensurabile con lo schema analitico poi usato dall'umano | Media |
| A3 | `Q2 (Y_N) - 1.3.1-1.3.2 - Analisi risposta 1.3.docx`, `H3 -> L3` | Granularita del coding non allineata al bisogno finale | il LLM riconosce esplicitamente che il grafico dell'umano, costruito sulle sue categorie JSON, e "piu fine" e "piu adatto a una presentazione di ricerca" rispetto alla lettura precedente del LLM | suggerisce che la prima lettura del follow-up aperto era utile come sintesi, ma non ancora al livello di dettaglio richiesto nel contesto reale della presentazione | Media |

## Dettaglio dei casi principali

### P1. Allegato dato per presente ma non disponibile al LLM

**Documento:** `4 - Analisi preliminare questionario.docx`  
**Istante:** `H2 -> L2`

L'umano scrive che allega un JSON di esempio per la domanda 1.2 e chiede report grafici per la presentazione. Il LLM risponde pero che, in quel momento, vede solo il CSV grezzo e non il JSON.

Questo e un problema di interazione perche:

- l'umano considera l'azione di allegare gia completata
- il LLM non riceve davvero l'oggetto necessario
- il dialogo si sposta dal compito analitico al recupero del contesto mancante

Non e un errore metodologico del LLM, ma e un punto di attrito netto nel flusso collaborativo.

### P2. Conteggio sbagliato dovuto al formato del JSON

**Documento:** `4 - Analisi preliminare questionario.docx`  
**Istante:** `H3 -> L3 -> H4 -> L4`

Dopo che l'umano incolla il JSON, il LLM produce un primo output e dichiara `122` risposte categorizzate. L'umano interviene con una correzione esplicita: vede `137` righe nel file e chiede di ricontrollare.

Questo e il caso piu forte dell'intero corpus, perche abbiamo tutti i segnali classici di una risposta insoddisfacente:

- il LLM produce un numero specifico
- l'umano lo mette in dubbio
- l'umano formula una richiesta di revisione
- il LLM riconosce il problema e lo spiega

La causa individuata dal LLM e tecnica ma rilevante: il JSON era strutturato come mappa `{risposta: categoria}` e quindi le chiavi duplicate venivano sovrascritte. Il primo output era dunque formalmente coerente col parser, ma sbagliato per l'uso analitico.

Qui il problema di interazione e duplice:

- il LLM non ha inizialmente inferito che il formato JSON era pericoloso per dati con risposte duplicate
- l'umano e stato costretto a fare controllo manuale e a riaprire il punto

### P3. Dall'esempio singolo allo strumento riusabile

**Documento:** `4 - Analisi preliminare questionario.docx`  
**Istante:** `H5 -> L5`

Dopo la correzione del conteggio, l'umano cambia piano e dice chiaramente che gli sarebbe "piu comodo" uno script Python per visualizzare le frequenze di tutte le domande aperte.

Questo passaggio segnala un problema piu sottile: la risposta del LLM aveva risolto il caso specifico, ma non il vero bisogno di lavoro dell'utente, cioe un flusso ripetibile e scalabile.

Il problema non e che il LLM avesse risposto "male" in senso stretto. Il problema e che la forma della soluzione non era ancora centrata sul task pratico reale.

## Pattern ricorrenti osservati

### 1. Attrito da granularita analitica

In piu punti il LLM fornisce una sintesi utile ma piu aggregata di quella che l'umano poi usa davvero per la presentazione o per i confronti successivi.

Questo succede soprattutto nelle domande aperte:

- il LLM tende a una prima codifica sintetica
- l'umano o un collega costruiscono poi categorie piu fini
- la collaborazione deve riallinearsi a quello schema piu analitico

Il segnale piu chiaro e in `Q2`, quando il LLM dice esplicitamente che il grafico dell'umano e migliore del proprio riassunto iniziale per un contesto di ricerca.

### 2. Attrito da trasferimento di artefatti

I problemi non nascono solo dall'interpretazione del contenuto, ma anche dal passaggio di oggetti tra umano e LLM:

- JSON dato per allegato ma non visibile
- JSON in formato formalmente valido ma semanticamente inadatto
- immagini usate come base di confronto invece di file strutturati

Questo pattern suggerisce che una parte importante dell'attrito non e cognitiva, ma infrastrutturale: il dialogo perde efficienza quando l'oggetto di lavoro non arriva nel formato piu robusto.

### 3. Attrito da riuso del risultato

Alcune risposte del LLM sono utili come "one-shot", ma non immediatamente riusabili come procedura.

Quando l'umano chiede:

- grafici per la presentazione
- script Python
- confronti per sottogruppi

sta spesso traducendo una risposta ancora discorsiva in un bisogno operativo piu stabile. Questo e un segnale importante: non sempre il primo output del LLM e nel formato di lavoro piu utile.

## Anomalie documentali da non confondere con i problemi di interazione

Ci sono anche due anomalie che conviene segnalare, ma che non vanno lette come veri problemi collaborativi.

### D1. Inversione di ruolo nel testo esportato

In `Q2 (Y_N) - 1.3.1-1.3.2 - Analisi risposta 1.3.docx`, il primo blocco LLM si apre con una frase del tipo "Ti allego il file CSV...", come se fosse il modello ad allegare il file all'umano. E quasi certamente un artefatto di esportazione o di montaggio del testo, non un problema sostanziale di interazione.

### D2. Confine dei tag non sempre perfetto

Nello stesso documento `Q2`, la richiesta successiva sui sottogruppi appare inglobata nel blocco LLM finale invece di comparire come un nuovo blocco `<human>`. Anche questo sembra un problema di esportazione del documento piu che del dialogo in se.

## Valutazione sintetica

I problemi di interazione piu robusti del corpus non sono molti, ma sono istruttivi. I piu chiari sono tre:

1. un problema di disponibilita del contesto
2. un problema di interpretazione tecnica del formato dati
3. un problema di allineamento tra soluzione locale e bisogno operativo reale

Il caso piu importante e senza dubbio il **conteggio sbagliato del JSON con chiavi duplicate**, perche li l'umano deve davvero contestare il risultato e chiedere una revisione.

Gli altri attriti sono piu "soft", ma mostrano bene dove la collaborazione tende a rompersi o rallentarsi:

- quando il formato dell'artefatto non e robusto
- quando la risposta del LLM e troppo aggregata rispetto all'uso finale
- quando l'output e corretto ma non ancora riusabile come procedura

## Conclusione

Se si guarda alla cronologia delle chat in `docs`, il punto in cui emerge piu chiaramente un problema di interazione in senso forte e:

**`4 - Analisi preliminare questionario.docx`, nel passaggio `H3 -> L3 -> H4 -> L4`, dove l'umano e costretto a far ricontrollare il conteggio del JSON e il LLM riconosce un errore dovuto alla sovrascrittura delle chiavi duplicate.**

Accanto a questo, emergono alcuni attriti secondari ma ricorrenti:

- allegati non effettivamente disponibili al modello
- differenza di granularita tra coding del LLM e coding usato poi dall'umano
- risposte utili ma non ancora nel formato operativo piu comodo

Questi momenti non invalidano il lavoro svolto, ma sono i punti piu utili da osservare se l'obiettivo e studiare la qualita dell'interazione umano-LLM piu che il solo contenuto delle analisi.
