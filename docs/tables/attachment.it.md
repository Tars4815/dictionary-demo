# Tabella: `attachment`

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella memorizza le informazioni e i dettagli relativi a un allegato.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco dell'allegato | `3` | PK | No | [...] |
| `damage_id` | BIGINT | Chiave esterna che fa riferimento a un danno segnalato | [...] | FK | No | Punta all'id dell'entità [damage](damage.md) |
| `date` | TIMESTAMP | [...] | - | - | No | - |
| `size` | BIGINT | [...] | - | - | No | - |
| `description` | VARCHAR | [...] | - | - | No | - |
| `name` | VARCHAR | [...] | - | - | No | - |
| `type` | VARCHAR | [...] | - | - | No | - |
| `data` | BIGINT | [...] | - | - | No | - |

## Relazioni

* **Documenti** [`damage`](damage.md)