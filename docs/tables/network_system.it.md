# Tabella: `network_system`

**Descrizione (IT):** Questa tabella rappresenta i sistemi infrastrutturali a rete (es. reti di trasporto, elettriche o di telecomunicazione). Nell'architettura di ereditarietà del database, funge da sottotipo diretto della tabella `enterprise`. Non memorizza colonne descrittive ridondanti; utilizza invece una chiave primaria condivisa per ereditare tutti gli attributi di alto livello (come nome, posizione, tipo di gestione e geometria) dal suo record `enterprise` genitore.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco del sistema a rete | `8` | PK, FK | No | Chiave primaria che funge anche da Chiave Esterna con riferimento a `enterprise.id` |

## Relazioni

* **Eredita da (Sottotipo di):** [`enterprise`](enterprise.md). La tabella `network_system` è un'estensione specializzata della tabella `enterprise`.
* **Contiene:** Pur non essendo collegata direttamente tramite un `network_system_id`, un sistema a rete possiede asset infrastrutturali attraverso la colonna `enterprise_id` nella tabella `component`. Questi componenti includono spesso sottotipi di rete specializzati come:
    * `transport_network_component` (componenti reti di trasporto)
    * `electrical_network_component` (componenti reti elettriche)
    * `tlc_network_component` (componenti reti di telecomunicazioni)
    * `network_service` (servizi di rete)

!!! tip "Dove si trova il resto dei dati?"
    Per trovare il nome, la posizione geografica (`geometry`, `town`, `country`) o i dettagli sulla proprietà di un sistema a rete, devi unire (join) questa tabella con il record `enterprise` che condivide lo stesso identico `id`.

## Query di Esempio

Recupera un elenco di tutti i sistemi a rete, inclusi i loro nomi, città e coordinate spaziali, unendo la tabella con l'entità genitore `enterprise`:

```sql
SELECT 
    n.id, 
    e.name, 
    e.town, 
    ST_AsText(e.geometry) as coordinates 
FROM 
    network_system n
JOIN 
    enterprise e ON n.id = e.id
WHERE 
    e.type = 'NETWORK_SYSTEM';
```