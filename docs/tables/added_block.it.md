# Tabella: `added_block`

!!! info "Nome diverso nell'interfaccia web (GUI)"
    Nel backend PostgreSQL questa tabella si chiama `added_block`, come indicato nel titolo della pagina. Nell'interfaccia della web-app compare come **Added block**. Tutti gli alias sono riportati nella [tabella di corrispondenza](../backend-to-gui.md).

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella rappresenta i corpi aggiunti degli edifici. Nell'architettura di ereditarietà del database, funge da sottotipo diretto della tabella [`component`](component.md). Non memorizza colonne descrittive ridondanti: usa invece una chiave primaria condivisa per ereditare tutti gli attributi di alto livello (come nome, posizione, tipo di gestione e geometria) dal record genitore `component`.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco del corpo aggiunto | `42` | PK, FK | No | Chiave primaria che funge anche da chiave esterna verso `component.id` |
| `position` | VARCHAR | [...] | `EXTERNAL` | - | No | [...] |
| `vertical_mat` | VARCHAR | [...] | [...] | - | No | [...] |
| `horizontal_mat` | VARCHAR | [...] | [...] | - | No | [...] |
| `n_floor` | BIGINT | Numero di piani del corpo aggiunto | `2` | - | No | [...] |
| `total_height` | BIGINT | Altezza totale del corpo aggiunto in [unità di misura] | `200` | - | No | [...] |
| `floor_surface` | BIGINT | Superficie totale dei piani del corpo aggiunto in [unità di misura] | `200` | - | No | [...] |
| `floor_height` | BIGINT | Altezza totale dei piani del corpo aggiunto in [unità di misura] | `200` | - | No | [...] |
| `function` | VARCHAR | [...] | [...] | - | No | [...] |
| `previous_survey` | VARCHAR | [...] | [...] | - | No | [...] |

## Relazioni

* **Eredita da (sottotipo di):** [`component`](component.md). La tabella `added_block` è un'estensione specializzata della tabella `component`.
* **Appartiene a:** [`enterprise`](enterprise.md) (Un sottotipo di componente è collegato a una sola impresa)
* **Ha molti:** `damage` (Un sottotipo di componente può subire più danni nel tempo)

!!! tip "Dove si trova il resto dei dati?"
    Per trovare il nome, la posizione geografica (`geometry`, `town`, `country`) o i dettagli sulla proprietà di un record added_block, devi unire questa tabella con il record `component` che condivide lo stesso `id`.

## Query di esempio

Recupera un elenco di tutti i corpi aggiunti, includendo nomi, comuni e coordinate spaziali, unendo la tabella con la sua entità genitore `component`:

```sql
SELECT 
    ab.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    added_block ab
JOIN 
    component c ON ab.id = c.id
WHERE 
    c.component_kind  = 'ADDED_BLOCK';
```