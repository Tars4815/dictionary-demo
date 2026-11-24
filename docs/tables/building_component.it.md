# Tabella: `building_component`

!!! info "Nome diverso nell'interfaccia web (GUI)"
    Nel backend PostgreSQL questa tabella si chiama `building_component`, come indicato nel titolo della pagina. Nell'interfaccia della web-app compare come **Principal structure**. Tutti gli alias sono riportati nella [tabella di corrispondenza](../backend-to-gui.md).

!!! warning "Traduzione assistita dall'IA"
    Questa pagina è stata tradotta con l'assistenza dell'intelligenza artificiale e può contenere imprecisioni. La versione inglese è il riferimento. I nomi delle tabelle e degli attributi sono identici in tutte le lingue perché corrispondono a quelli dell'implementazione PostgreSQL.

**Descrizione (IT):** Questa tabella memorizza le caratteristiche strutturali, economiche e fisiche degli edifici, inclusi i dettagli costruttivi, i tipi di materiale e le dimensioni. Nell'architettura di ereditarietà del database, funge da sottotipo diretto della tabella [`component`](component.md). Non memorizza colonne descrittive ridondanti: usa invece una chiave primaria condivisa per ereditare tutti gli attributi di alto livello (come nome, posizione e geometria) dal record genitore `component`.

## Struttura delle colonne

| Colonna | Tipo di dato | Definizione | Valore di esempio | Vincolo? | Geometria? | Commenti |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identificativo univoco del componente edilizio | `42` | PK, FK | No | Chiave primaria che funge anche da chiave esterna verso `component.id` |
| `principal` | BOOLEAN | Indica se si tratta del componente edilizio principale | `true` | - | No | [...] |
| `subtype` | VARCHAR(255) | [...] | [...] | - | No | [...] |
| `public_service_code` | VARCHAR(255) | [...] | [...] | - | No | [...] |
| `heritage_tier` | VARCHAR(255) | [...] | [...] | - | No | [...] |
| `year` | INTEGER | Anno di costruzione | `1999` | - | No |  |
| `quality` | VARCHAR(255) | Qualità complessiva | `GOOD` | - | No | Valori possibili: POOR, GOOD, ACCEPTABLE, NOT_IDENTIFIABLE |
| `conservation` | VARCHAR(255) | Stato di conservazione dell'edificio | `POORLY_MANTAINED` | CHECK | No | Valori possibili: POORLY_MANTAINED, MODERATELY_MAINTAINED, WELL_MAINTAINED, NOT_IDENTIFIABLE |
| `retrofitting` | VARCHAR(255) | Stato dell'adeguamento strutturale (retrofitting) | `NOT_IDENTIFIABLE` | CHECK | No | Valori possibili: NONE, VERTICAL, HORIZONTAL, COMPLETE, NOT_IDENTIFIABLE, ecc. |
| `regularity` | VARCHAR(255) | Regolarità della struttura | `NOT_IDENTIFIABLE` | CHECK | No | Valori possibili: NOT_REGULAR, COMPLETELY_REGULAR, ecc. |
| `inhabitants` | INTEGER | Numero di abitanti dell'edificio considerato | `6` | - | No |  |
| `construction_cost` | INTEGER | Costo di costruzione | `500000` | - | No |  |
| `economic_value` | INTEGER | Valore economico | `1000000` | - | No |  |
| `vertical_mat` | VARCHAR(255) | Materiale da costruzione delle strutture verticali | `NOT_IDENTIFIABLE` | CHECK | No | Valori possibili: STEEL, WOOD, MASONRY_ADOBE, ecc. |
| `horizontal_mat` | VARCHAR(255) | Materiale da costruzione delle strutture orizzontali | `MASONRY_ADOBE` | CHECK | No | Valori possibili: STEEL, WOOD, MASONRY_ADOBE, ecc. |
| `roof_mat` | VARCHAR(255) | Materiale dell'elemento di copertura | `NOT_IDENTIFIABLE` | CHECK | No | Valori possibili: STEEL, WOOD, MASONRY_ADOBE, ecc. |
| `build_position` | VARCHAR(255) | Posizione dell'edificio | `SINGLE_DETACHED` | CHECK | No | Valori possibili: SINGLE_DETACHED, SEMI_DETACHED, ROW, NOT_IDENTIFICABLE |
| `ground_floor` | VARCHAR(255) | Tipologia del piano terra | `OPEN` | CHECK | No | Valori possibili: OPEN, CLOSE, NOT_IDENTIFIABLE |
| `n_floors` | INTEGER | Numero di piani fuori terra | `3` | - | No |  |
| `floor_height` | INTEGER | Altezza media dei piani | `4` | - | No |  |
| `n_under_floors` | INTEGER | Numero di piani interrati | `1` | - | No |  |
| `floor_area` | INTEGER | Superficie dei piani in metri quadrati | `1000` | - | No |  |
| `usage` | VARCHAR(255) | [...] | [...] | - | No | [...] |
| `foundation_typology` | VARCHAR(255) | Tipologia delle fondazioni | [...] | - | No | [...] |
| `main_use` | VARCHAR(255) | Uso principale dell'edificio | [...] | - | No | [...] |

## Relazioni

* **Eredita da (sottotipo di):** [`component`](component.md). La tabella `building_component` è un'estensione specializzata della tabella `component`.
* **Appartiene a:** [`enterprise`](enterprise.md) (Un sottotipo di componente è collegato a una sola impresa)
* **Ha molti:** `damage` (Un sottotipo di componente può subire più danni nel tempo)

!!! tip "Dove si trova il resto dei dati?"
    Per trovare il nome, la posizione geografica (`geometry`, `town`, `country`) o i dettagli sulla proprietà di un componente edilizio, devi unire questa tabella con il record `component` che condivide lo stesso `id`.

## Query di esempio

Recupera un elenco di tutti i componenti edilizi, includendo nomi, comuni e coordinate spaziali, unendo la tabella con la sua entità genitore `component`:

```sql
SELECT 
    bc.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    building_component bc
JOIN 
    component c ON bc.id = c.id
WHERE 
    c.component_kind = 'BUILDING_COMPONENT';
```
