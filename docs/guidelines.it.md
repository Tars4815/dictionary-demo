# Linee guida per contribuire

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

Grazie per aiutarci a mantenere il dizionario dati accurato e aggiornato! 

Una buona documentazione è un lavoro di squadra. Non è necessario essere sviluppatori, saper programmare o conoscere Git per contribuire a questo progetto. Tutti gli aggiornamenti dei contenuti sono gestiti tramite un semplice foglio di calcolo.

---

## Il flusso di lavoro

Aggiornare il dizionario richiede solo tre semplici passaggi:

1. **Scarica il template:** Recupera l'ultima versione del template Excel del dizionario dati dalla nostra cartella condivisa del team.
2. **Compila i dati:** Aggiungi o aggiorna le righe corrispondenti alle tabelle e alle colonne del database che stai documentando.
3. **Invia per la pubblicazione:** Invia il file Excel aggiornato al team tecnico. Eseguiremo un processo automatico per convertire il tuo foglio di calcolo nelle pagine web che vedi qui.

---

## Come compilare il template Excel

Ogni foglio del file Excel rappresenta una singola tabella del database. Per ogni colonna di quella tabella, fornisci i seguenti dettagli:

* **Column:** Il nome tecnico esatto del campo nel database (ad es. `user_id`, `geom`, `created_at`).
* **Data type:** Il formato del dato (ad es. `VARCHAR(255)`, `UUID`, `POINT`, `INTEGER`).
* **Definition (IT) & Definition (EN):** Una descrizione chiara e comprensibile anche ai non addetti ai lavori di ciò che la colonna rappresenta. Compila sia la colonna italiana sia quella inglese, per supportare la nostra piattaforma bilingue.
* **Example value:** Un esempio realistico del dato, per aiutare gli altri a capirne il formato (ad es. `john.doe@email.com` o `POINT(12.49 41.89)`).
* **Constraint?:** Indica eventuali regole del database, come `PK` (chiave primaria), `FK` (chiave esterna) o `NOT NULL`.
* **Geometry?:** Specifica se il campo contiene dati spaziali (ad es. `Yes - EPSG:4326` o `No`).
* **Comments (IT) & Comments (EN):** Qualsiasi contesto aggiuntivo, logica di business o avvertenza su come usare o interpretare questo dato.

!!! warning "Mantieni la formattazione semplice"
    Evita formattazioni Excel complesse, come celle unite, colori personalizzati delle celle o più righe all'interno di una stessa cella. Il testo semplice garantisce la conversione più fluida verso la piattaforma web!

---

## Inviare le modifiche

Quando il tuo file Excel è pronto e rivisto:

* Carica la nuova versione nell'unità condivisa designata.
* Avvisa il team di amministrazione del database via email o tramite la nostra chat interna.
* Il team elaborerà il file e le tue modifiche saranno pubblicate nel dizionario dati nel giro di pochi minuti!