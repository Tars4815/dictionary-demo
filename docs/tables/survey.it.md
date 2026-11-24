# Tabella: `survey`

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella memorizza le informazioni e i dettagli relativi a uno specifico rilevamento di valutazione dei danni, condotto a seguito di un evento di rilievo.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco del rilevamento | `3` | PK | No | [...] |
| `created_on` | TIMESTAMP | Momento di esecuzione del rilevamento di valutazione | [...] | NOT NULL | No | [...] |
| `enterprise_id` | BIGINT | Chiave esterna che fa riferimento a un'impresa | [...] | FK | No | Punta all'id dell'entità [enterprise](enterprise.md) |
| `event_id` | BIGINT | Momento di esecuzione del rilevamento di valutazione | [...] | FK | No | Punta all'id dell'entità [event](event.md) |

## Relazioni

Poiché `survey` è una delle entità centrali dello schema, ha numerose relazioni:

* **Segnala** [`damage`](damage.md)
* **È collegato a** [`enterprise`](enterprise.md)
* **Segue un** [`event`](event.md)