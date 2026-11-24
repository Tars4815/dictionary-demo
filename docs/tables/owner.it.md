# Tabella: `owner`

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa entità memorizza gli attributi universali di alto livello, come l'identificazione e i contatti, per i record dei proprietari.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco del proprietario | `3` | PK | No | - |
| `email` | VARCHAR | Indirizzo email del proprietario | `example@mail.com` | - | No | - |
| `fiscal_code` | VARCHAR | Codice fiscale del proprietario | `AB0123CDEF` | - | No | Il numero di caratteri e la configurazione possono variare da Paese a Paese |
| `full_name` | VARCHAR | Nome completo del proprietario | `John Doe` | - | No | - |
| `phone` | VARCHAR | Numero di telefono e prefisso internazionale del proprietario | `+390123456789` | - | No | - |

## Relazioni

* **Possiede:** [`enterprise`](enterprise.md) (Un proprietario possiede un'impresa). Questa relazione molti-a-molti è mediata dalla tabella di collegamento [`enterprise_owner`](enterprise_owner.md).

## Query di esempio

Recupera un elenco di tutti i proprietari, mostrando il loro nome e i loro contatti specifici:

```sql
SELECT *
FROM 
    owner o
ORDER BY 
    o.full_name ASC;
```

