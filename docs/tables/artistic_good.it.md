# Tabella: `artistic_good`

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella rappresenta i beni artistici. Nell'architettura di ereditarietà del database, funge da sottotipo diretto della tabella [`component`](component.md). Non memorizza colonne descrittive ridondanti: usa invece una chiave primaria condivisa per ereditare tutti gli attributi di alto livello (come nome, posizione, tipo di gestione e geometria) dal record genitore `component`.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco del bene artistico | `42` | PK, FK | No | Chiave primaria che funge anche da chiave esterna verso `component.id` |
| `kind` | VARCHAR | [...]] | [...] | - | No | [...] |

## Relazioni

* **Eredita da (sottotipo di):** [`component`](component.md). La tabella `artistic_good` è un'estensione specializzata della tabella `component`.
* **Appartiene a:** [`enterprise`](enterprise.md) (Un sottotipo di componente è collegato a una sola impresa)
* **Ha molti:** `damage` (Un sottotipo di componente può subire più danni nel tempo)

!!! tip "Dove si trova il resto dei dati?"
    Per trovare il nome, la posizione geografica (`geometry`, `town`, `country`) o i dettagli sulla proprietà di un bene artistico, devi unire questa tabella con il record `component` che condivide lo stesso `id`.

## Query di esempio

Recupera un elenco di tutti i beni artistici, includendo nomi, comuni e coordinate spaziali, unendo la tabella con la sua entità genitore `enterprise`:

```sql
SELECT 
    ag.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    added_block ag
JOIN 
    component c ON ag.id = c.id
WHERE 
    c.component_kind  = 'ARTISTIC_GOOD';
```
