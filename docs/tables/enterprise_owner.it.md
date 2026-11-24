# Tabella: `enterprise_owner`

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa entità funge da tabella di collegamento per la relazione molti-a-molti tra [`enterprise`](enterprise.md) e [`owner`](owner.md).

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `enterprise_id` | BIGINT | Identificativo dell'impresa | `3` | FK | No | Fa riferimento alla tabella `enterprise` |
| `owner_id` | BIGINT | Identificativo del proprietario | `8` | FK | No | Fa riferimento alla tabella `owner` |


