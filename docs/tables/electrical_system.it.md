# Tabella: `electrical_system`

!!! info "Nome diverso nell'interfaccia web (GUI)"
    Nel backend PostgreSQL questa tabella si chiama `electrical_system`, come indicato nel titolo della pagina. Nell'interfaccia della web-app compare come **Lifelines - Electrical**. Tutti gli alias sono riportati nella [tabella di corrispondenza](../backend-to-gui.md).

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella rappresenta i sistemi di rete elettrica. Nell'architettura di ereditarietà del database, funge da sottotipo diretto della tabella [`network_system`](network_system.md). Non memorizza colonne descrittive ridondanti: usa invece una chiave primaria condivisa per ereditare tutti gli attributi di alto livello (come nome, posizione, tipo di gestione e geometria) dal record genitore `network_system`, che a sua volta è figlio di un record [`enterprise`](enterprise.md).

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco del sistema di rete elettrica | `8` | PK, FK | No | Chiave primaria che funge anche da chiave esterna verso `network_system.id` e `enterprise.id` |

## Relazioni

* **Eredita da (sottotipo di):** [`network_system`](network_system.md). La tabella `electrical_system` è un'estensione specializzata della tabella `network_system`.
* **Contiene:** Pur non essendo collegato direttamente tramite `electrical_system_id`, un sistema elettrico possiede asset infrastrutturali attraverso la colonna `enterprise_id` della tabella `component`. Questi componenti includono spesso sottotipi specializzati, come:
    * `electrical_network_component`

!!! tip "Dove si trova il resto dei dati?"
    Per trovare il nome, la posizione geografica (`geometry`, `town`, `country`) o i dettagli sulla proprietà di un sistema di rete, devi unire questa tabella con il record `enterprise` che condivide lo stesso `id`.

## Query di esempio

Recupera un elenco di tutti i sistemi elettrici, includendo nomi, comuni e coordinate spaziali, unendo la tabella con la sua entità genitore `network_system` - `enterprise`:

```sql
SELECT 
    es.id, 
    e.name, 
    e.town, 
    ST_AsText(e.geometry) as coordinates 
FROM 
    electrical_system es
JOIN 
    enterprise e ON es.id = e.id
WHERE 
    e.type = 'ELECTRICAL_SYSTEM';