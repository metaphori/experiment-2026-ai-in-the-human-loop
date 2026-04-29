# Stima di completezza e precisione del background iniziale nelle chat della prima fase

## Perimetro

Questa stima riguarda la **prima fase di analisi del questionario**, dal **11 aprile 2025** al **7 maggio 2025**, conclusa con la preparazione della prima presentazione per il gruppo di ricerca.

Fonte principale:
- `2025-survey-analysis/CT_Survey_2025_GPT_chats.xlsx`

Supporto interpretativo:
- `2025-survey-analysis/phase1_salient_chats.md`

## Obiettivo

Stimare **quanto il contesto iniziale fornito dall'umano al LLM** fosse:

- **completo**, cioe ricco degli elementi necessari a inquadrare bene il compito;
- **preciso**, cioe formulato in modo sufficientemente chiaro, specifico e operativo.

## Scala usata

Per entrambe le dimensioni uso una scala da **1 a 5**:

- **1** = molto basso
- **2** = basso
- **3** = medio
- **4** = medio-alto
- **5** = alto

## Criteri di valutazione

### Completezza del contesto iniziale

Valuta se il prompt iniziale include abbastanza elementi tra questi:

- obiettivo del compito;
- oggetto di analisi;
- dominio o popolazione;
- materiali o dati allegati;
- output atteso;
- vincoli pratici, temporali o metodologici.

### Precisione del contesto iniziale

Valuta se il prompt iniziale:

- pone una richiesta ben delimitata;
- riduce l'ambiguita;
- specifica bene cosa deve fare il modello;
- usa categorie o variabili riconoscibili;
- rende chiaro il formato dell'output desiderato.

## Giudizio complessivo

Se considero l'intera prima fase, il contesto iniziale fornito al LLM risulta:

- **Completezza complessiva stimata: 3.6/5**
- **Precisione complessiva stimata: 4.1/5**

## Interpretazione sintetica

Il pattern principale e questo:

- **all'inizio della fase** il contesto e spesso **abbastanza preciso ma poco completo**;
- **nelle chat operative e di presentazione** il contesto diventa **molto piu completo e resta abbastanza preciso**;
- **nelle chat grafiche e tecniche** la precisione resta buona, ma parte del contesto resta implicita e affidata ad allegati, immagini o aspettative condivise, quindi la completezza non e sempre massima.

In breve: **la precisione media del prompting iniziale e piu alta della completezza**. L'umano sa spesso cosa chiedere, ma all'inizio non fornisce ancora tutto il contesto necessario per una risposta pienamente situata.

## Lettura per cluster di chat

## 1. Fase esplorativa-metodologica iniziale

Chat principali:
- 2025-04-11 | `Analisi questionari aperti`
- 2025-04-14 | `Analisi qualitativa vs quantitativa`
- 2025-04-16 | `Analisi dati questionario artigianato`

Stima:
- **Completezza: 2.0/5**
- **Precisione: 3.9/5**

Perche:
- le domande sono chiare e centrate;
- il bisogno metodologico e esplicito;
- ma il contesto sul questionario reale e ancora parziale;
- mancano spesso dettagli su campione, struttura completa del questionario, urgenza, deliverable finale e vincoli analitici.

Interpretazione:
- il modello riceve domande ben formulate, ma ancora poco "situate" nel caso concreto;
- il contesto iniziale serve piu a **orientarsi** che a **istruire operativamente** il modello.

## 2. Fase operativa sulle domande aperte e sui materiali

Chat principali:
- 2025-04-15 | `New chat`
- 2025-04-30 | `Unire file JSON risposte`
- 2025-05-03 | `Riorganizzazione categorie JSON`
- 2025-05-03 | `Voci con Manualità JSON`

Stima:
- **Completezza: 3.3/5**
- **Precisione: 4.0/5**

Perche:
- quando il task e stretto, il prompt e molto preciso;
- nel caso del 15 aprile il contesto e addirittura ricco di dati, vincoli e formato atteso;
- in altre chat operative, pero, parte del contesto e delegata agli allegati e al lavoro gia svolto in precedenza;
- questo rende la richiesta comprensibile, ma non sempre autosufficiente.

Interpretazione:
- il contesto iniziale migliora molto rispetto alla fase esplorativa;
- tuttavia in alcune chat il modello deve "ereditarne" una parte dagli allegati o dalla continuita implicita del progetto.

## 3. Fase di costruzione del primo report e della presentazione

Chat principali:
- 2025-04-30 | `Presentazione risultati ricerca`
- 2025-05-03 | `Creazione presentazione questionario studenti`

Stima:
- **Completezza: 5.0/5**
- **Precisione: 4.3/5**

Perche:
- qui il background iniziale e molto ricco;
- vengono specificati campione, contesto scolastico, obiettivi della rilevazione, materiali allegati, finalita del lavoro e struttura desiderata dell'output;
- il modello riceve quindi sia il quadro generale sia il deliverable atteso.

Limite residuo:
- la richiesta e ricca, ma anche ampia;
- alcune priorita restano aperte, ad esempio profondita analitica, rapporto tra descrizione e interpretazione, o ruolo del LaTeX nei risultati.

Interpretazione:
- e il punto della fase 1 in cui il contesto iniziale e piu completo;
- il prompting diventa quasi un mini-brief di progetto.

## 4. Fase grafica e rifinitura tecnica

Chat principali:
- 2025-05-05 | `Grafico barre orizzontale`
- 2025-05-06 | `Grafico a barre frequenze`
- 2025-05-06 | `Grafico a barre artigianato`

Stima:
- **Completezza: 4.0/5**
- **Precisione: 4.1/5**

Perche:
- le richieste sono concrete e orientate a un artefatto ben identificabile;
- l'utente specifica stile desiderato, aggregazione in "Altro", presenza di frequenze e percentuali;
- tuttavia molto contesto e affidato a immagini, grafici di riferimento e aspettative visive implicite.

Interpretazione:
- il contesto iniziale e abbastanza buono, ma non sempre totalmente esplicito;
- infatti i follow-up mostrano che alcuni vincoli visuali importanti emergono solo dopo la prima risposta.

## 5. Chat di confine verso la fase statistica successiva

Chat principali:
- 2025-05-07 | `Analisi statistica questionario`

Stima:
- **Completezza: 5.0/5**
- **Precisione: 4.5/5**

Perche:
- il prompt iniziale include obiettivo, script di partenza, sottogruppi, regole di normalizzazione e criteri di accorpamento;
- il compito e operativo, tecnico e molto ben delimitato.

Limite residuo:
- alcuni requisiti emergono comunque dopo, ad esempio ordine delle colonne, esportazione XLSX e leggibilita del risultato;
- quindi il contesto iniziale e molto forte, ma non ancora esaustivo al 100%.

Interpretazione:
- dal punto di vista del prompting iniziale, questa e la chat piu matura della prima fase;
- mostra una forte crescita della capacita di istruire il modello in modo tecnico.

## Stima su alcune chat chiave

| Chat | Completezza | Precisione | Nota sintetica |
|---|---:|---:|---|
| 2025-04-11 `Analisi questionari aperti` | 2.0 | 4.0 | Domanda chiara, ma poco contesto sul caso concreto |
| 2025-04-14 `Analisi qualitativa vs quantitativa` | 1.0 | 4.0 | Richiesta molto precisa, quasi nessun background sul progetto |
| 2025-04-15 `New chat` | 4.5 | 4.5 | Task e output molto ben specificati, con dati inclusi |
| 2025-04-16 `Analisi dati questionario artigianato` | 3.0 | 4.0 | Domanda situata nel dominio, ma ancora generale |
| 2025-04-30 `Unire file JSON risposte` | 4.0 | 4.0 | Obiettivo tecnico chiaro, buon contesto sui materiali |
| 2025-04-30 `Presentazione risultati ricerca` | 5.0 | 4.0 | Brief ricco e ben contestualizzato |
| 2025-05-03 `Creazione presentazione questionario studenti` | 5.0 | 4.5 | Contesto molto completo e output ben definito |
| 2025-05-03 `Riorganizzazione categorie JSON` | 2.5 | 3.5 | Richiesta comprensibile ma dipendente da allegati e contesto implicito |
| 2025-05-06 `Grafico a barre frequenze` | 4.0 | 4.0 | Richiesta concreta, ma con parte del contesto visivo implicito |
| 2025-05-07 `Analisi statistica questionario` | 5.0 | 4.5 | Prompt tecnico maturo e molto ben specificato |

## Punti di forza del contesto iniziale nella fase 1

- L'obiettivo locale del prompt e spesso chiaro anche quando il background generale e ridotto.
- Col progredire della fase aumenta la capacita di definire output desiderati, materiali allegati e vincoli pratici.
- Nelle chat piu mature l'umano fornisce al LLM un contesto quasi da brief professionale.

## Punti deboli del contesto iniziale nella fase 1

- Nelle prime chat manca spesso il quadro complessivo del progetto di ricerca.
- Alcune richieste si appoggiano molto a contesto implicito, immagini o file allegati non riassunti verbalmente.
- Diversi vincoli importanti emergono solo dopo la prima risposta del modello, segno che il contesto iniziale non era ancora del tutto esternalizzato.

## Giudizio finale

Se devo sintetizzare in una frase:

> Nella prima fase, il contesto iniziale fornito al LLM e mediamente **piu preciso che completo**: le richieste sono spesso formulate in modo chiaro e mirato, ma soprattutto nelle chat iniziali non includono ancora tutto il background necessario a collocare pienamente il compito. La completezza cresce sensibilmente nelle chat operative e diventa alta nelle richieste orientate alla presentazione e agli script statistici.

## Formula breve riusabile nel paper

> The initial context provided to ChatGPT during Phase 1 was overall more precise than complete. Early prompts were typically clear in their immediate request but relatively sparse in project-level background, whereas later prompts became increasingly rich in contextual information, attached materials, expected outputs, and operational constraints. This suggests a progressive maturation in the user's ability to frame the task for the model.
