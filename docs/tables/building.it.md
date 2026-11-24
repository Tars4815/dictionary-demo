# Tabella: `building`

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella rappresenta gli edifici. Nell'architettura di ereditarietà del database, funge da sottotipo diretto della tabella [`enterprise`](enterprise.md). Non memorizza colonne descrittive ridondanti: usa invece una chiave primaria condivisa per ereditare tutti gli attributi di alto livello (come nome, posizione, tipo di gestione e geometria) dal record genitore `enterprise`.

Le caratteristiche strutturali, economiche e fisiche di un edificio (anno di costruzione, materiali, numero di piani, costo e così via) sono memorizzate nella tabella [`building_component`](building_component.md).

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco dell'edificio | `3` | PK, FK | No | Chiave primaria che funge anche da chiave esterna verso `enterprise.id` |

## Relazioni

* **Eredita da (sottotipo di):** [`enterprise`](enterprise.md). La tabella `building` è un'estensione specializzata della tabella `enterprise`.
* **Contiene:** Pur non essendo collegato direttamente tramite `building_id`, un edificio possiede le proprie parti fisiche attraverso la colonna `enterprise_id` della tabella `component`. Questi componenti includono spesso sottotipi specializzati, come:
    * [`building_component`](building_component.md)
    * [`added_block`](added_block.md)
    * [`building_functionality`](building_functionality.md)

!!! tip "Dove si trova il resto dei dati?"
    Per trovare il nome, la posizione geografica (`geometry`, `town`, `country`) o la partita IVA di un edificio, devi unire questa tabella con il record `enterprise` che condivide lo stesso `id`. Le caratteristiche strutturali ed economiche si trovano in `building_component`, collegata all'edificio tramite `component.enterprise_id`.

## Query di esempio

Recupera le caratteristiche di ciascun edificio unendo il relativo record di impresa con i suoi componenti edilizi:

```sql
SELECT
    e.name,
    e.town,
    bc.n_floors,
    bc.construction_cost,
    bc.economic_value
FROM
    building b
JOIN
    enterprise e ON b.id = e.id
JOIN
    component c ON c.enterprise_id = e.id
JOIN
    building_component bc ON bc.id = c.id
WHERE
    e.type = 'BUILDING';
```
