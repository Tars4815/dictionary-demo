# Tabella: `event`

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella memorizza le informazioni e i dettagli relativi a un evento di rilievo specifico.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco dell'evento | `3` | PK | No | [...] |
| `date` | TIMESTAMP | Momento in cui si verifica l'evento | [...] | - | No | [...] |
| `date_end` | TIMESTAMP | Momento di conclusione dell'evento | [...] | - | No | [...] |
| `parent_event_id` | BIGINT | Riferimento in caso di evento multiplo | [...] | FK | No | Punta all'id dell'entità [event](event.md) |
| `name` | VARCHAR | Nome dell'evento | `Storm Example` | - | No | - |
| `severity` | VARCHAR | Livello di gravità dell'evento | [...] | - | No | - |
| `type` | VARCHAR | Tipo di evento | [...] | - | No | - |
| `country` | VARCHAR | Paese in cui si trova l'evento | `Italy` | - | No | - |
| `state` | VARCHAR | Stato o regione in cui si trova l'evento | `Lazio` | - | No | - |
| `county` | VARCHAR | Contea o provincia in cui si trova l'evento | `Rome` | - | No | - |
| `town` | VARCHAR | Comune in cui si trova l'evento | `Rome` | - | No | - |
| `hamlet` | VARCHAR | Frazione o località in cui si trova l'evento | `Trastevere` | - | No | - |
| `road` | VARCHAR | Via in cui si trova l'evento | `Via Appia` | - | No | - |
| `house_number` | VARCHAR | Numero civico dell'evento | `10` | - | No | - |
| `postcode` | VARCHAR | Codice postale dell'evento | `00100` | - | No | - |
| `geometry` | GEOMETRY | Rappresentazione spaziale dell'evento | [...] | - | Sì | - |
| `coordinates_inferred` | BOOLEAN | Indica se le coordinate dell'evento sono state dedotte anziché misurate direttamente | [...] | - | No | - |

## Relazioni

* **Ha molti:** [`survey`](survey.md) (Un evento può essere seguito da più rilevamenti di valutazione dei danni)
* **È parte di / ha parti:** [`event`](event.md) tramite `parent_event_id`. Un evento multiplo può essere suddiviso in eventi figli che puntano all'evento genitore.
