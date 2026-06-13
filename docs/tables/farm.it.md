# Tabella: `farm`

**Descrizione (IT):** Questa tabella rappresenta le imprese agricole. Nell'architettura di ereditarietà del database, funge da sottotipo diretto della tabella[`enterprise`](enterprise.md). Non memorizza colonne descrittive ridondanti; utilizza invece una chiave primaria condivisa per ereditare tutti gli attributi di alto livello (come nome, posizione, tipo di gestione e geometria) dal suo record `enterprise` genitore.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco dell'azienda agricola | `42` | PK, FK | No | Chiave primaria che funge anche da Chiave Esterna con riferimento a `enterprise.id` |

## Relazioni

* **Eredita da (Sottotipo di):** [`enterprise`](enterprise.md). La tabella `farm` è un'estensione specializzata della tabella `enterprise`.
* **Contiene:** Pur non essendo collegata direttamente tramite un `farm_id`, un'azienda agricola possiede asset agricoli attraverso la colonna `enterprise_id` nella tabella `component`. Questi componenti includono spesso sottotipi agricoli specializzati come:
    * `crop` (coltura)
    * `livestock` (bestiame)
    * `agriculture_product` (prodotto agricolo)
    * `structure` (struttura, es. fienili, serre)
    * `machinery` (macchinari, es. trattori)

!!! tip "Dove si trova il resto dei dati?"
    Per trovare il nome, la posizione geografica (`geometry`, `town`, `country`) o i dettagli sulla proprietà di un'azienda agricola, devi unire (join) questa tabella con il record `enterprise` che condivide lo stesso identico `id`.

## Query di Esempio

Recupera un elenco di tutte le aziende agricole, inclusi i loro nomi, città e coordinate spaziali, unendo la tabella con l'entità genitore `enterprise`:

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