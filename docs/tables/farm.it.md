# Tabella: `farm`

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella rappresenta le imprese agricole. Nell'architettura di ereditarietà del database, funge da sottotipo diretto della tabella [`enterprise`](enterprise.md). Non memorizza colonne descrittive ridondanti: usa invece una chiave primaria condivisa per ereditare tutti gli attributi di alto livello (come nome, posizione, tipo di gestione e geometria) dal record genitore `enterprise`.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco dell'azienda agricola | `42` | PK, FK | No | Chiave primaria che funge anche da chiave esterna verso `enterprise.id` |

## Relazioni

* **Eredita da (sottotipo di):** [`enterprise`](enterprise.md). La tabella `farm` è un'estensione specializzata della tabella `enterprise`.
* **Contiene:** Pur non essendo collegata direttamente tramite `farm_id`, un'azienda agricola possiede asset agricoli attraverso la colonna `enterprise_id` della tabella `component`. Questi componenti includono spesso sottotipi agricoli specializzati, come:
    * [`agriculture_product`](agriculture_product.md) e i suoi sottotipi [`crop`](crop.md) e [`stored`](stored.md)
    * [`livestock`](livestock.md)
    * [`fixed_asset`](fixed_asset.md) e i suoi sottotipi (ad es. [`machinery`](machinery.md), come i trattori)

!!! tip "Dove si trova il resto dei dati?"
    Per trovare il nome, la posizione geografica (`geometry`, `town`, `country`) o altri dettagli di un'azienda agricola, devi unire questa tabella con il record `enterprise` che condivide lo stesso `id`.

## Query di esempio

Recupera un elenco di tutte le aziende agricole, includendo nomi, comuni e coordinate spaziali, unendo la tabella con la sua entità genitore `enterprise`:

```sql
SELECT 
    f.id, 
    e.name, 
    e.town, 
    ST_AsText(e.geometry) as coordinates 
FROM 
    farm f
JOIN 
    enterprise e ON f.id = e.id
WHERE 
    e.type = 'FARM';
```
