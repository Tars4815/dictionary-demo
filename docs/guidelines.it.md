# Linee Guida per Contribuire

Grazie per aiutarci a mantenere il Dizionario Dati accurato e aggiornato! 

Una buona documentazione è un lavoro di squadra. Non è necessario essere sviluppatori, saper programmare o conoscere Git per contribuire a questo progetto. Tutti gli aggiornamenti dei contenuti sono gestiti tramite un semplice foglio di calcolo.

---

## Il Flusso di Lavoro

Aggiornare il dizionario richiede solo tre semplici passaggi:

1. **Scarica il Template:** Recupera l'ultima versione del template Excel del Dizionario Dati dalla nostra cartella condivisa del team.
2. **Compila i Dati:** Aggiungi o aggiorna le righe corrispondenti alle tabelle e alle colonne del database che stai documentando.
3. **Invia per la Pubblicazione:** Invia il file Excel aggiornato al team tecnico. Eseguiremo un processo automatico per convertire il tuo foglio di calcolo nelle pagine web che vedi qui.

---

## Come Compilare il Template Excel

Ogni foglio nel file Excel rappresenta una singola tabella del database. Per ogni colonna in quella tabella, fornisci i seguenti dettagli:

* **Column:** Il nome tecnico esatto del campo nel database (es. `user_id`, `geom`, `created_at`).
* **Data type:** Il formato dei dati (es. `VARCHAR(255)`, `UUID`, `POINT`, `INTEGER`).
* **Definition (IT) & Definition (EN):** Una descrizione chiara e comprensibile di cosa rappresenta la colonna. Ti preghiamo di compilare sia la colonna italiana che quella inglese per supportare la nostra piattaforma multilingua.
* **Example value:** Un esempio realistico del dato per aiutare gli altri a capirne il formato (es. `mario.rossi@email.com` o `POINT(12.49 41.89)`).
* **Constraint?:** Annota eventuali regole del database, come `PK` (Primary Key/Chiave Primaria), `FK` (Foreign Key/Chiave Esterna), o `NOT NULL`.
* **Geometry?:** Specifica se il campo contiene dati spaziali (es. `Sì - EPSG:4326` o `No`).
* **Comments (IT) & Comments (EN):** Qualsiasi contesto aggiuntivo, logica di business o avvertenza su come questo dato dovrebbe essere utilizzato o interpretato.

!!! warning "Mantieni la Formattazione Semplice"
    Ti preghiamo di evitare l'uso di formattazioni complesse in Excel, come celle unite, colori personalizzati o più righe all'interno di una singola cella. Il testo semplice garantisce una conversione senza intoppi sulla piattaforma web!

---

## Inviare le Modifiche

Una volta che il tuo file Excel è pronto e revisionato:

* Carica la nuova versione nel drive condiviso designato.
* Avvisa il team di amministrazione del database tramite email o la nostra chat interna.
* Il team elaborerà il file e le tue modifiche saranno online sul Dizionario Dati in pochi minuti!