# Tabella: `crop`

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella rappresenta le colture. Nell'architettura di ereditarietà del database, funge da sottotipo diretto della tabella [`agriculture_product`](agriculture_product.md). Non memorizza colonne descrittive ridondanti: usa invece una chiave primaria condivisa per ereditare tutti gli attributi di alto livello (come nome, posizione, tipo di gestione e geometria) dal record genitore `component`.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco del record della coltura | `42` | PK, FK | No | Chiave primaria che funge anche da chiave esterna verso `agriculture_product.id` e, a sua volta, verso `component.id` |
| `area_planted` | BIGINT | [...] | [...] | - | No | [...] |
| `category` | VARCHAR | [...] | [...] | - | No | [...] |
| `growth` | VARCHAR | [...] | [...] | - | No | [...] |
| `duration` | VARCHAR | [...] | [...] | - | No | [...] |

## Relazioni

* **Eredita da (sottotipo di):** [`agriculture_product`](agriculture_product.md). La tabella `crop` è un'estensione specializzata della tabella `agriculture_product`.
* **Appartiene a:** [`enterprise`](enterprise.md) (Un sottotipo di componente è collegato a una sola impresa)
* **Ha molti:** `damage` (Un sottotipo di componente può subire più danni nel tempo)

!!! tip "Dove si trova il resto dei dati?"
    Per trovare il nome, la posizione geografica (`geometry`, `town`, `country`) o i dettagli sulla proprietà di una coltura, devi unire questa tabella con il record `component` che condivide lo stesso `id`.

## Query di esempio

Recupera un elenco di tutte le colture, includendo nomi, comuni e coordinate spaziali, unendo la tabella con la sua entità genitore `component`:

```sql
SELECT
    c.id,
    c.area_planted,
    c.category,
    ap.year_production 
FROM 
    crop c join agriculture_product ap on c.id = ap.id 
where ap.subtype = 'CROP'
```