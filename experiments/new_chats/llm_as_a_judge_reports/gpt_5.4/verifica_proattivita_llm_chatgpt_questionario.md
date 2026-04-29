# Verifica dei momenti in cui sarebbe stata utile una maggiore proattivita del LLM nelle chat sul questionario

## Obiettivo

Questo report verifica se, e in quali momenti, nelle chat contenute in `docs` sarebbe stato utile che il LLM fosse piu proattivo nel:

- chiedere dati aggiuntivi
- chiedere chiarimenti
- chiedere conferme metodologiche
- fermare l'analisi finche il contesto non fosse sufficientemente definito

Per "proattivita utile" intendo quindi non un semplice fare piu domande, ma il porre quelle domande che avrebbero ridotto:

- rischio di errore
- ambiguita del task
- disallineamento tra output del LLM e bisogno dell'utente
- fragilita metodologica delle conclusioni

Nel report uso la notazione `Hn/Ln` per indicare, dentro ciascun documento, il turno umano e il turno LLM corrispondente.

## Criterio di valutazione

Ho considerato che una domanda proattiva del LLM sarebbe stata utile soprattutto quando mancava almeno una di queste informazioni:

1. formato corretto dei dati o semantica dell'artefatto allegato
2. regola di codifica o granularita desiderata dell'analisi
3. conferma delle colonne o delle variabili davvero da usare
4. regole decisionali per confronti inferenziali e sottogruppi
5. chiarimento tra output esplorativo, output da slide e output da report di ricerca

## Risposta breve

**Si: nel corpus ci sono diversi momenti in cui sarebbe stato utile che il LLM fosse piu proattivo.**

I momenti piu importanti sono sei. I tre piu critici sono:

1. **prima di usare il JSON come se fosse un contenitore affidabile di casi**
2. **prima di analizzare l'item Likert con colonne lasciate come placeholder**
3. **prima di eseguire test di differenza tra sottogruppi senza concordare un piccolo protocollo**

## Momenti principali individuati

| ID | Documento e istante | Quanto sarebbe stato utile | Cosa mancava | Cosa il LLM avrebbe dovuto chiedere |
| --- | --- | --- | --- | --- |
| M1 | `1-4`, in particolare `1 - Analisi questionario calzaturiero.docx`, `H1 -> L1` e `4 - Analisi preliminare questionario.docx`, `H1 -> L1` | Utile | obiettivo analitico finale piu preciso | se il focus fosse descrittivo o inferenziale; quale deliverable servisse; quali domande fossero prioritarie |
| M2 | `4 - Analisi preliminare questionario.docx`, `H3 -> L3` | Essenziale | semantica del JSON e unita di conteggio | se il JSON rappresentasse casi unici o potesse contenere duplicati; quale fosse il numero atteso di righe; se ogni riga valesse come una risposta |
| M3 | `Q1 (OT) - 2.3...`, `H1 -> L1` e `Q2 (Y_N)...`, `H2 -> L2` | Molto utile | granularita e regole della codifica qualitativa | se servissero categorie molto sintetiche o piu fini; se assegnare un solo codice o piu codici; se esistesse gia un codebook umano |
| M4 | `Q1 (OT) - 2.3...`, `H2 -> L2` | Molto utile | sorgente strutturata del grafico da confrontare | se l'utente avesse anche il file dati o il JSON sottostante, invece della sola immagine |
| M5 | `Q6 (Lik.Inv) - 8.5...`, `H1 -> L1` | Essenziale | elenco esplicito delle colonne da usare | quali sottocolonne fossero davvero rilevanti; se l'elenco individuato dal LLM fosse corretto e completo |
| M6 | `Q1/Q2/Q3/Q3-2/Q4/Q5/Q6`, al momento della richiesta sui sottogruppi (`H3 -> L3` o equivalente) | Essenziale | mini protocollo inferenziale condiviso | se l'analisi fosse esplorativa o confirmatoria; quale alpha usare; se correggere per confronti multipli; come ricodificare e filtrare i sottogruppi |

## Analisi dettagliata

### M1. All'inizio delle chat generali: sarebbe stato utile chiarire meglio l'obiettivo finale

Nelle prime chat il contesto e buono, ma resta abbastanza aperto. Il LLM riceve informazioni su:

- il dataset
- il tema del questionario
- la scarsa esperienza iniziale dell'utente
- il bisogno di una prima analisi

Quello che pero manca, almeno all'inizio, e una piccola negoziazione del compito finale. Una o due domande proattive avrebbero aiutato il LLM a tarare meglio la risposta sin da subito.

### Domande che il LLM avrebbe potuto fare

- `Ti serve una prima lettura descrittiva o vuoi gia impostare una fase inferenziale?`
- `L'output finale sara una presentazione breve, un report scritto o una base per analisi successive?`
- `Ci sono gia alcune domande del questionario che consideri prioritarie?`

### Perche sarebbe stato utile

Perche queste informazioni emergono piu chiaramente solo dopo, distribuite su piu chat. Se il LLM le avesse raccolte subito, avrebbe potuto:

- proporre una pipeline piu mirata
- distinguere meglio tra output esplorativo e output piu rigoroso
- evitare parte della successiva riallocazione del lavoro

## M2. Prima di contare il JSON: il LLM avrebbe dovuto fermarsi e chiedere come interpretare il file

Questo e il caso piu forte del corpus.

Nel documento `4 - Analisi preliminare questionario.docx`, dopo che l'umano incolla il JSON con le associazioni risposta -> categoria, il LLM procede direttamente al conteggio e produce un risultato poi contestato dall'utente.

L'errore nasce dal fatto che il LLM tratta il JSON come mappa standard, ma il contenuto analitico richiedeva di capire se:

- potessero esserci chiavi duplicate
- ogni riga rappresentasse un caso
- il numero di righe atteso fosse coerente con i conteggi ottenuti

### Domande che il LLM avrebbe dovuto fare prima di contare

- `Questo JSON e una mappa tecnica o va trattato come lista di casi?`
- `Le stesse risposte testuali possono comparire piu volte?`
- `Quante righe ti aspetti che vengano contate?`
- `Vuoi che verifichi subito se il formato puo perdere occorrenze duplicate?`

### Perche sarebbe stato utile

Perche qui la proattivita non sarebbe stata un lusso, ma una prevenzione diretta di un errore che infatti si e verificato.

## M3. Prima della codifica delle aperte: sarebbe stato utile concordare la granularita del coding

Nelle domande aperte, soprattutto in `Q1` e nel follow-up di `Q2`, il LLM produce una prima codifica sintetica. In seguito, pero, l'umano usa schemi piu fini, spesso gia organizzati in JSON o in grafici propri.

Questo segnala che il LLM ha risposto bene a un compito generico, ma non ha chiesto abbastanza su **quanto fine** dovesse essere la categorizzazione.

### Domande proattive che avrebbero aiutato

- `Vuoi categorie molto sintetiche da primo report o un codebook piu fine da ricerca?`
- `Preferisci una sola categoria prevalente per risposta o 1-2 codici per caso?`
- `Vuoi che tenga una categoria separata per "non sa", ironico o fuori tema?`
- `Hai gia un sistema di categorie umano/collegiale a cui devo allinearmi?`

### Perche sarebbe stato utile

Perche avrebbe ridotto il rischio di produrre un output formalmente corretto ma poi non pienamente riusabile o non allineato allo schema analitico effettivamente adottato dall'utente.

## M4. Nel confronto tra grafici: sarebbe stato meglio chiedere i dati sorgente, non ricostruire dall'immagine

Nel documento `Q1`, l'utente chiede di confrontare il grafico prodotto dal LLM con un grafico gia creato da lui. Il LLM procede ricostruendo i conteggi a partire dalle etichette visibili nell'immagine.

La procedura funziona, ma e fragile. Qui una proattivita minima avrebbe migliorato molto la robustezza del confronto.

### Domande che il LLM avrebbe dovuto fare

- `Hai anche il JSON o il CSV che sta dietro al grafico?`
- `Vuoi che confronti i dati sorgente invece di ricostruire i valori dall'immagine?`
- `Le categorie del tuo grafico sono definitive oppure solo una versione provvisoria?`

### Perche sarebbe stato utile

Perche il confronto sarebbe stato:

- piu affidabile
- meno dipendente dalla leggibilita dell'immagine
- piu facile da riusare anche nei passaggi successivi

## M5. Sull'item Likert inverso: il placeholder delle colonne richiedeva una domanda immediata

Nel prompt iniziale di `Q6` compare esplicitamente `[COLUMN NAME(S)]`. Nonostante questo, il LLM procede da solo identificando le cinque sottovoci nel CSV.

La ricostruzione e plausibile, ma il prompt, preso alla lettera, segnala che manca una parte essenziale del contesto.

### Domande che il LLM avrebbe dovuto fare

- `Confermi che le sottocolonne da analizzare sono queste cinque?`
- `Vuoi includerle tutte o solo alcune?`
- `Le etichette che ho trovato nel CSV corrispondono esattamente al tuo item di interesse?`

### Perche sarebbe stato utile

Perche qui il rischio non e tanto il calcolo, ma l'uso delle colonne sbagliate o di un perimetro analitico non confermato dall'utente.

## M6. Prima dei test sui sottogruppi: sarebbe stato utile concordare un mini protocollo

In molte chat, dopo l'analisi descrittiva, l'utente chiede di verificare se esistano differenze significative tra:

- genere
- corso di studi
- anno di corso

Il LLM esegue i confronti, spesso con buone cautele a posteriori. Pero quasi mai si ferma prima a raccogliere alcune decisioni metodologiche fondamentali.

### Domande che il LLM avrebbe dovuto fare

- `Vuoi che questa analisi sia esplorativa o la vuoi gia impostare come test inferenziale piu formale?`
- `Che soglia di significativita vuoi usare?`
- `Vuoi una correzione per confronti multipli, soprattutto nei casi con molte opzioni o sottovoci?`
- `Come vuoi trattare le risposte anomale o non classificabili nei sottogruppi?`
- `Vuoi che riporti solo p-value o anche misure di effetto e limiti di numerosita?`

### Perche sarebbe stato utile

Perche il cuore del problema non e solo "fare un test", ma concordare prima:

- il perimetro dei dati
- la natura esplorativa o meno dell'analisi
- il livello di cautela interpretativa

Senza questa mini negoziazione, il LLM si prende implicitamente decisioni che sarebbe stato meglio condividere con l'utente.

## Dove il LLM e stato gia parzialmente proattivo, ma troppo tardi

In alcuni casi il LLM diventa proattivo, ma solo dopo che il rischio e gia diventato concreto.

### Esempio 1: JSON con chiavi duplicate

Nel caso del JSON delle aperte, il LLM capisce il problema delle chiavi duplicate solo dopo che l'utente contesta il conteggio. La proattivita sarebbe stata piu utile prima del primo conteggio, non dopo.

### Esempio 2: JSON delle categorie in `Q2`

Nel confronto del grafico della 1.3.2, il LLM avverte solo alla fine che un JSON con le risposte come chiavi potrebbe perdere casi duplicati. Anche qui il warning arriva, ma sarebbe stato piu utile come domanda iniziale di verifica.

### Esempio 3: sottogruppi

In diversi item il LLM dichiara durante l'esecuzione che le variabili dei sottogruppi sono sporche o non perfettamente pulite. Una mossa piu proattiva sarebbe stata fermarsi un attimo prima dei test per chiedere all'utente come volesse ricodificare o escludere quei casi.

## Valutazione sintetica

Nel corpus la maggiore proattivita del LLM sarebbe stata utile soprattutto in tre classi di situazione:

1. **quando il formato del dato poteva cambiare il conteggio**
2. **quando il task chiedeva una scelta metodologica non esplicitata**
3. **quando il LLM stava per fare inferenze che implicavano assunzioni condivise solo in parte**

La priorita piu alta non era quindi "fare piu domande in generale", ma fare poche domande mirate nei punti giusti.

## Conclusione

Se si guarda alle chat in `docs`, il LLM avrebbe tratto beneficio da una maggiore proattivita in modo selettivo, non continuo.

I momenti in cui sarebbe stato davvero utile chiedere chiarimenti sono quelli in cui:

- il formato dei dati era ambiguo
- lo schema di codifica non era concordato
- le colonne o le sottovoci non erano completamente specificate
- i test sui sottogruppi richiedevano decisioni metodologiche condivise

Il caso piu netto e il **JSON delle domande aperte**, dove una sola domanda preventiva sul formato dei casi avrebbe probabilmente evitato l'errore di conteggio emerso dopo.

Il secondo caso piu importante e l'**analisi dei sottogruppi**, dove una breve negoziazione iniziale sul protocollo avrebbe reso le analisi piu trasparenti, difendibili e allineate all'intenzione dell'utente.
