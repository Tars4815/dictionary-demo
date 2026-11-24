# Tabella: `economic_loss`

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella memorizza i costi associati a un danno segnalato: gli importi stimati, approvati e finali.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco del record di perdita economica | `3` | PK | No | [...] |
| `damage_id` | BIGINT | Chiave esterna che fa riferimento a un danno segnalato | [...] | FK | No | Punta all'id dell'entità [damage](damage.md) |
| `approved_cost` | DOUBLE PRECISION | Costo approvato per il danno | - | - | No | - |
| `estimated_cost` | DOUBLE PRECISION | Costo stimato del danno | - | - | No | - |
| `final_cost` | DOUBLE PRECISION | Costo finale del danno | - | - | No | - |
| `type_of_cost` | VARCHAR | Tipo di costo | - | - | No | - |

## Relazioni

* **Fa riferimento a:** [`damage`](damage.md) tramite `damage_id`. La perdita economica è il risultato monetario di un danno segnalato.

## Query di esempio

Recupera i costi registrati per ciascun danno:

```sql
SELECT 
    d.id AS damage_id, 
    el.type_of_cost, 
    el.estimated_cost, 
    el.approved_cost, 
    el.final_cost 
FROM 
    economic_loss el
JOIN 
    damage d ON el.damage_id = d.id;
```
