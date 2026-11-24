# Tabella: `network_system`

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella rappresenta i sistemi di rete infrastrutturali (ad es. reti di trasporto, elettriche o di telecomunicazione). Nell'architettura di ereditarietà del database, funge da sottotipo diretto della tabella [`enterprise`](enterprise.md). Non memorizza colonne descrittive ridondanti: usa invece una chiave primaria condivisa per ereditare tutti gli attributi di alto livello (come nome, posizione, tipo di gestione e geometria) dal record genitore `enterprise`.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco del sistema di rete | `8` | PK, FK | No | Chiave primaria che funge anche da chiave esterna verso `enterprise.id` |

## Relazioni

* **Eredita da (sottotipo di):** [`enterprise`](enterprise.md). La tabella `network_system` è un'estensione specializzata della tabella `enterprise`.
* **Ha sottotipi (ereditarietà):** Le tabelle seguenti ereditano da `network_system` (e, tramite essa, da `enterprise`) e condividono il suo `id`:
    * [`electrical_system`](electrical_system.md)
    * [`tlc_system`](tlc_system.md)
    * [`transport_system`](transport_system.md)
* **Contiene:** Pur non essendo collegato direttamente tramite `network_system_id`, un sistema di rete possiede asset infrastrutturali attraverso la colonna `enterprise_id` della tabella `component`. Questi componenti includono spesso sottotipi specializzati, come:
    * `transport_network_component`
    * `electrical_network_component`
    * `tlc_network_component`
    * `network_service`

!!! tip "Dove si trova il resto dei dati?"
    Per trovare il nome, la posizione geografica (`geometry`, `town`, `country`) o altri dettagli di un sistema di rete, devi unire questa tabella con il record `enterprise` che condivide lo stesso `id`.

## Query di esempio

Recupera un elenco di tutti i sistemi di rete, includendo nomi, comuni e coordinate spaziali, unendo la tabella con la sua entità genitore `enterprise`:

```sql
SELECT 
    n.id, 
    e.name, 
    e.town, 
    e.type,
    ST_AsText(e.geometry) as coordinates 
FROM 
    network_system n
JOIN 
    enterprise e ON n.id = e.id;
```
