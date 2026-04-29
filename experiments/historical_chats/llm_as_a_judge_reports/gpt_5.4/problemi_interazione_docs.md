# Identificazione degli istanti con problemi di interazione nelle chat di `dataset/docs`

## Perimetro

Questa analisi riguarda le chat contenute in `dataset/docs`, con particolare attenzione alla cronologia dei turni:

- `<human></human>`: richieste o follow-up dell'umano;
- `<LLM></LLM>`: risposte del modello.

L'obiettivo è individuare gli **istanti in cui emergono problemi di interazione**, cioè momenti in cui la sequenza dei turni suggerisce che la risposta precedente del LLM non sia stata sufficiente, aderente o eseguibile.

## Criteri usati per riconoscere un problema di interazione

Ho considerato come segnali forti di problema:

1. **Domanda ripetuta o quasi identica** dopo una risposta del LLM.
2. **Riformulazione correttiva** del requisito da parte dell'umano.
3. **Segnalazione esplicita di errore** durante l'esecuzione del codice generato dal LLM.
4. **Richiesta di riallineamento** rispetto a un criterio esterno o a un output atteso non rispettato.
5. **Misunderstanding**: il LLM risponde, ma l'umano precisa che intendeva altro.

Non ho contato come problemi:

- semplici estensioni naturali del task;
- aggiunta di nuovi file o nuovi obiettivi non dovuti a un errore del LLM;
- affinamenti ordinari che non implicano una mancata aderenza precedente.

## Sintesi complessiva

Nel corpus emergono **9 istanti/episodi ad alta confidenza** e **1 episodio a confidenza media**.

I problemi osservati si concentrano in quattro famiglie:

- **non aderenza ai vincoli del prompt**;
- **gestione incompleta di template o file allegati**;
- **codice generato non eseguibile o fragile**;
- **risposta tecnicamente corretta ma poco interpretabile rispetto al bisogno reale dell'umano**.

Le chat più problematiche sono:

- `3.2`
- `3.3`
- `3.4`
- `4.2`

## Episodi ad alta confidenza

### 1. `3.2`, turno umano 5

**Istante**

Dopo che il LLM ha prodotto un primo hand-off PowerPoint, l'umano scrive:

> `Ti chiedo due cose: 1) Puoi utilizzare il template che ti ho allegato? 2) Puoi esplicitare le domande del questionario dove serve...`

**Perché è un problema di interazione**

Il vincolo del template era già implicito nel primo messaggio della chat, che allegava il file delle slide. Il follow-up mostra che la risposta precedente non aveva soddisfatto almeno due requisiti centrali:

- uso del template allegato;
- esplicitazione delle domande del questionario nelle slide.

**Tipo di problema**

`Mancata aderenza ai vincoli iniziali del prompt`

---

### 2. `3.2`, turno umano 9

**Istante**

Dopo che il LLM segnala di vedere ancora un file `.ppt` e chiede un `.pptx`, l'umano risponde:

> `Presentazione-tesi-Barry-Bassi-18-07-2024-LM.pptx ... Se tento di allegare il file pptx mi rispondi che non è possibile estrarre testi dal file...`

**Perché è un problema di interazione**

Qui emerge una frizione concreta tra bisogno dell'utente e gestione degli allegati/template:

- il LLM non riesce a lavorare subito sul template voluto;
- l'umano deve spiegare il problema dell'upload e cambiare strategia;
- il focus si sposta dal compito al superamento di un ostacolo tecnico.

**Tipo di problema**

`Fricizione su file/template e gestione dell'input`

---

### 3. `3.3`, turno umano 3

**Istante**

L'umano ripete quasi **identicamente** il prompt iniziale:

> `Puoi generare un grafico a barre orizzontali ...`

dopo una prima risposta del LLM che aveva già fornito un codice.

**Perché è un problema di interazione**

La ripetizione quasi verbatim è un segnale classico di insoddisfazione o di mancata consegna percepita. Anche senza una contestazione esplicita, la cronologia suggerisce che la prima risposta non abbia risolto il bisogno.

**Tipo di problema**

`Domanda ripetuta dopo risposta non ritenuta sufficiente`

---

### 4. `3.3`, turno umano 5

**Istante**

L'umano riporta un traceback completo:

> `ottengo questo errore: ... AttributeError ...`

dopo aver provato il codice ricevuto.

**Perché è un problema di interazione**

È un caso netto di problema esecutivo:

- il LLM ha prodotto codice plausibile;
- il codice non funziona nell'ambiente concreto dell'utente;
- l'utente deve interrompere il flusso per fare debugging.

**Tipo di problema**

`Codice generato non portabile / non eseguibile nell'ambiente dell'utente`

---

### 5. `3.4`, turno umano 3

**Istante**

Anche qui l'umano ripete quasi identicamente il prompt iniziale sul grafico:

> `Puoi generarmi un grafico a barre ...`

**Perché è un problema di interazione**

La ripetizione segnala che la prima risposta non è stata sufficiente o non è stata fruita come output utilizzabile. Il segnale è rafforzato dal turno successivo del LLM che contiene esplicitamente:

> `Errore nell’analisi`

**Tipo di problema**

`Fallimento della prima generazione / necessità di rilanciare il task`

---

### 6. `3.4`, episodi dal turno umano 15 al turno umano 23

**Istante**

Nella seconda parte della chat l'umano riporta una **catena di traceback** successivi:

- `KeyError: '1.1'`
- errore `NAN/INF not supported`
- `TypeError: ExcelWriter.__new__() got an unexpected keyword argument 'options'`
- nuovo `KeyError` sulle colonne
- `ValueError` da `chi2_contingency`

**Perché è un problema di interazione**

Questo è l'episodio di frizione tecnica più forte dell'intero corpus. Non si tratta di un singolo bug, ma di una sequenza di fix successivi che non stabilizzano il codice al primo colpo.

Il pattern osservato è:

1. il LLM propone uno script;
2. l'utente lo esegue;
3. emerge un nuovo errore;
4. il LLM corregge solo il punto appena emerso;
5. il ciclo si ripete.

**Tipo di problema**

`Debugging reattivo e progressivo di codice fragile`

---

### 7. `4.2`, turno umano 7

**Istante**

Dopo che il LLM promette export `XLSX` e report completi, l'umano scrive:

> `Non genera gli XLSX: ...`

**Perché è un problema di interazione**

Qui l'insoddisfazione è esplicita e direttamente collegata a un deliverable promesso dal LLM ma non ottenuto in esecuzione.

**Tipo di problema**

`Deliverable promesso ma non prodotto`

---

### 8. `4.2`, turno umano 13

**Istante**

Dopo aver già chiesto:

> `Anche nella tabella di analisi chi-quadro sarebbe utile avere le colonne relative ai valori confrontati`

l'umano torna sul punto e lo riformula:

> `Anche nella tabella di analisi chi-quadro sarebbe utile avere le colonne relative ai valori confrontati Puoi modificare lo script per ottenere dati più facilmente interpretabili?`

**Perché è un problema di interazione**

È un caso molto chiaro di riformulazione dopo risposta non centrata. Il primo follow-up non era soltanto "aggiungere colonne", ma migliorare l'interpretabilità del report. La ripetizione mostra che il LLM aveva risposto in modo incompleto rispetto al bisogno reale.

**Tipo di problema**

`Risposta formalmente pertinente ma non abbastanza aderente al bisogno interpretativo`

---

### 9. `4.2`, turno umano 17

**Istante**

Dopo che il LLM dichiara di aver reso uniformi i report, l'umano precisa:

> `Intendevo con questo ordine, come nel report aggregato: ...`

seguendo con l'ordine esatto desiderato delle categorie.

**Perché è un problema di interazione**

Il LLM aveva capito "ordine uniforme" in senso generico; l'umano intendeva invece **uno specifico ordine semantico**, già definito nel report aggregato. È quindi un misunderstanding sul requisito.

**Tipo di problema**

`Misunderstanding di un vincolo di ordinamento`

## Episodio a confidenza media

### 10. `2.3`, turno umano 3

**Istante**

Dopo la riassegnazione automatica delle categorie, l'umano chiede:

> `La tua riassegnazione delle categorie è allineata rispetto a questa analisi?`

**Perché è un possibile problema di interazione**

Non è una contestazione esplicita, ma suggerisce che la prima risposta non fosse ancora abbastanza affidabile o trasparente rispetto a un criterio esterno già disponibile all'umano.

Questo episodio segnala una criticità tipica:

- il LLM produce una riclassificazione;
- ma il criterio di "correttezza" non era stato completamente condiviso nel prompt iniziale;
- quindi serve un secondo passaggio di riallineamento.

**Tipo di problema**

`Criterio di validazione non completamente esplicitato`

**Confidenza**

`Media`, perché il follow-up può anche essere letto come controllo prudenziale e non necessariamente come insoddisfazione forte.

## Pattern trasversali emersi

### 1. Ripetizione della stessa richiesta come segnale forte

I casi di `3.3` e `3.4` sono i segnali più netti. Quando l'umano ripete quasi parola per parola la stessa richiesta, è molto probabile che la risposta precedente non sia stata percepita come risolutiva.

### 2. Molti problemi nascono dal passaggio da “risposta plausibile” a “artefatto eseguibile”

Il LLM produce spesso codice apparentemente corretto, ma i problemi emergono quando l'utente prova davvero a:

- eseguire lo script;
- esportare file;
- riusare template;
- gestire librerie/versioni/ambienti reali.

### 3. Una parte delle frizioni dipende da requisiti inizialmente impliciti

In alcune chat il requisito è presente, ma non è espresso con la massima rigidità operativa. Questo vale soprattutto per:

- uso del template PowerPoint;
- criterio di "allineamento" delle categorie;
- interpretabilità delle tabelle chi-quadro;
- ordine esatto delle categorie nei report.

### 4. Il LLM tende a correggere localmente l'errore, non sempre a ripensare il design complessivo

Nelle chat di debugging (`3.4`, `4.2`) si vede un pattern di correzione incrementale molto locale. Questo è utile nel breve, ma può aumentare i cicli di prova-errore quando il problema è strutturale.

## Valutazione finale

### Sintesi

Gli istanti di problema di interazione più affidabili si trovano soprattutto nelle chat in cui il LLM è usato per:

- generare codice Python;
- creare grafici riusabili;
- manipolare template PowerPoint;
- produrre export strutturati (`CSV`/`XLSX`) per l'analisi del questionario.

### Conclusione

La maggior parte dei problemi osservati non è dovuta a incomprensione totale del compito, ma a uno di questi quattro fattori:

1. **risposta non abbastanza aderente ai vincoli reali**;
2. **output non immediatamente eseguibile**;
3. **assunzioni implicite non condivise**;
4. **debugging troppo reattivo e poco sistemico**.

In formula breve:

**le frizioni emergono soprattutto quando il lavoro passa da una richiesta concettuale a un deliverable tecnico concreto.**

## Nota metodologica

Questa analisi si basa sui segnali osservabili nella cronologia delle chat. Quindi:

- gli episodi elencati sono quelli in cui il problema emerge chiaramente dai turni;
- non escludono la presenza di altri problemi non resi visibili dalla cronologia;
- non tutti i follow-up sono stati trattati come problemi, ma solo quelli che mostrano una discontinuità interpretabile come insoddisfazione, errore o riallineamento necessario.
