# Tabella: `agriculture_product`

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella rappresenta i prodotti agricoli. Nell'architettura di ereditarietà del database, funge da sottotipo diretto della tabella [`component`](component.md). Non memorizza colonne descrittive ridondanti: usa invece una chiave primaria condivisa per ereditare tutti gli attributi di alto livello (come nome, posizione, tipo di gestione e geometria) dal record genitore `component`.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco del prodotto agricolo | `42` | PK, FK | No | Chiave primaria che funge anche da chiave esterna verso `component.id` |
| `average_invested` | BIGINT | [...] | [...] | - | No | [...] |
| `expected_yield` | BIGINT | [...] | [...] | - | No | [...] |
| `gate_price` | BIGINT | [...] | [...] | - | No | [...] |
| `year_production` | BIGINT | [...] | [...] | - | No | [...] |
| `subtype` | VARCHAR | [...] | [...] | - | No | [...] |

## Relazioni

* **Eredita da (sottotipo di):** [`component`](component.md). La tabella `agriculture_product` è un'estensione specializzata della tabella `component`.
* **Ha sottotipi (ereditarietà):** Le tabelle seguenti ereditano da `agriculture_product` e condividono il suo `id`:
    * [`crop`](crop.md)
    * [`stored`](stored.md)
* **Appartiene a:** [`enterprise`](enterprise.md) (Un sottotipo di componente è collegato a una sola impresa)
* **Ha molti:** `damage` (Un sottotipo di componente può subire più danni nel tempo)

!!! tip "Dove si trova il resto dei dati?"
    Per trovare il nome, la posizione geografica (`geometry`, `town`, `country`) o i dettagli sulla proprietà di un prodotto agricolo, devi unire questa tabella con il record `component` che condivide lo stesso `id`.

## Query di esempio

Recupera un elenco di tutti i prodotti agricoli, includendo nomi, comuni e coordinate spaziali, unendo la tabella con la sua entità genitore `enterprise`:

```sql
SELECT 
    ap.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    agriculture_product ap
JOIN 
    component c ON ap.id = c.id
WHERE 
    c.component_kind  = 'AGRICULTURE_PRODUCT';
```
