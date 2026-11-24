# Tabella: `business`

!!! info "Nome diverso nell'interfaccia web (GUI)"
    Nel backend PostgreSQL questa tabella si chiama `business`, come indicato nel titolo della pagina. Nell'interfaccia della web-app compare come **Economic Activities - Business**. Tutti gli alias sono riportati nella [tabella di corrispondenza](../backend-to-gui.md).

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella rappresenta le imprese commerciali. Nell'architettura di ereditarietà del database, funge da sottotipo diretto della tabella [`enterprise`](enterprise.md). Non memorizza colonne descrittive ridondanti: usa invece una chiave primaria condivisa per ereditare tutti gli attributi di alto livello (come nome, posizione, tipo di gestione e geometria) dal record genitore `enterprise`.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco del record dell'attività commerciale | `8` | PK, FK | No | Chiave primaria che funge anche da chiave esterna verso `enterprise.id` |
| `share_capital` | BIGINT | Valore monetario totale dei fondi della società | [...] | - | No | [...] |
| `nace_section` | VARCHAR | Classificazione di primo livello dell'attività economica principale dell'impresa commerciale, secondo lo standard NACE | [...] | - | No | [...] |

## Relazioni

* **Eredita da (sottotipo di):** [`enterprise`](enterprise.md). La tabella `business` è un'estensione specializzata della tabella `enterprise`.
* **Contiene:** Pur non essendo collegato direttamente tramite `business_id`, un sistema di rete possiede asset infrastrutturali attraverso la colonna `enterprise_id` della tabella `component`. Questi componenti includono spesso sottotipi specializzati, come:
    * `business_operations`

!!! tip "Dove si trova il resto dei dati?"
    Per trovare il nome, la posizione geografica (`geometry`, `town`, `country`) o i dettagli sulla proprietà di un sistema di rete, devi unire questa tabella con il record `enterprise` che condivide lo stesso `id`.

## Query di esempio

Recupera un elenco di tutti i record delle attività commerciali, includendo nomi, comuni e coordinate spaziali, unendo la tabella con la sua entità genitore `enterprise`:

```sql
SELECT 
    b.id, 
    e.name, 
    e.town, 
    ST_AsText(e.geometry) as coordinates 
FROM 
    business b
JOIN 
    enterprise e ON b.id = e.id
WHERE 
    e.type = 'BUSINESS';
```