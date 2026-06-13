# Tabella: `building`

**Descrizione:** Questa tabella memorizza le caratteristiche strutturali, economiche e fisiche degli edifici, inclusi i dettagli di costruzione, i tipi di materiale e le dimensioni spaziali. Gli attributi categorici sono gestiti tramite vincoli CHECK direttamente nella definizione della tabella. Eredita le caratteristiche dell'entità più generica _Enterprise_.

## Struttura delle colonne

| Colonna             | Tipo di dato | Definizione                                        | Valore di esempio  | Vincolo?    | Geometria? | Commenti                                                                                    |
| :------------------ | :----------- | :------------------------------------------------- | :----------------- | :---------- | :--------- | :------------------------------------------------------------------------------------------ |
| `id`                | BIGINT       | Identificativo univoco dell'edificio               | `3`                | PK, FK      | No         | Chiave primaria che funge anche da chiave esterna per enterprise.id                         |
| `build_position`    | VARCHAR(255) | Posizione dell'edificio                            | `SINGLE_DETACHED`  | CHECK       | No         | Valori possibili: SINGLE_DETACHED, SEMI_DETACHED, ROW, NOT_IDENTIFICABLE                    |
| `conservation`      | VARCHAR(255) | Stato di conservazione dell'edificio               | `POORLY_MANTAINED` | CHECK       | No         | Valori possibili: POORLY_MANTAINED, MODERATELY_MANTAINED, WELL_MANTAINED, NOT_IDENTIFIABLE  |
| `construction_cost` | INTEGER      | Costo di costruzione stimato o effettivo           | `500000`           |             | No         |                                                                                             |
| `economic_value`    | INTEGER      | Valore economico o di mercato attuale              | `1000000`          |             | No         |                                                                                             |
| `floor_area`        | INTEGER      | Area totale dei piani (es. in metri quadrati)      | `1000`             |             | No         |                                                                                             |
| `floor_height`      | INTEGER      | Altezza media di un singolo piano                  | `7`                |             | No         |                                                                                             |
| `ground_floor`      | VARCHAR(255) | Tipologia/uso del piano terra                      | `OPEN`             | CHECK       | No         | Valori possibili: OPEN, CLOSE, NOT_IDENTIFIABLE                                             |
| `horizontal_mat`    | VARCHAR(255) | Materiale delle strutture orizzontali (es. solai)  | `NOT_IDENTIFIABLE` | CHECK       | No         | Valori possibili: STEEL, WOOD, MASONRY_ADOBE, ecc.                                          |
| `inhabitants`       | INTEGER      | Numero di persone che abitano o operano nell'edificio| `4`              |             | No         |                                                                                             |
| `n_floors`          | INTEGER      | Numero di piani fuori terra                        | `3`                |             | No         |                                                                                             |
| `n_under_floors`    | INTEGER      | Numero di piani interrati/seminterrati             | `1`                |             | No         |                                                                                             |
| `quality`           | VARCHAR(255) | Qualità complessiva dell'edificio                  | `NOT_IDENTIFIABLE` | CHECK       | No         | Valori possibili: POOR, GOOD, ACCEPTABLE, NOT_IDENTIFIABLE                                  |
| `regularity`        | VARCHAR(255) | Regolarità strutturale dell'edificio               | `NOT_IDENTIFIABLE` | CHECK       | No         | Valori possibili: NOT_REGULAR, COMPLETELY_REGULAR, ecc.                                     |
| `retrofitting`      | VARCHAR(255) | Interventi di adeguamento/miglioramento eseguiti   | `NONE`             | CHECK       | No         | Valori possibili: NONE, VERTICAL, HORIZONTAL, COMPLETE, NOT_IDENTIFIABLE, ecc.              |
| `roof_mat`          | VARCHAR(255) | Materiale dell'elemento di copertura (tetto)       | `NOT_IDENTIFIABLE` | CHECK       | No         | Valori possibili: STEEL, WOOD, MASONRY_ADOBE, ecc.                                          |
| `vertical_mat`      | VARCHAR(255) | Materiale delle strutture verticali                | `NOT_IDENTIFIABLE` | CHECK       | No         | Valori possibili: STEEL, WOOD, MASONRY_ADOBE, ecc.                                          |
| `year`              | INTEGER      | Anno di costruzione                                | `1999`             |             | No         |                                                                                             |

## Relazioni

- **Eredita da (Sottotipo di):** [`enterprise`](enterprise.md). La tabella `building` è un'estensione della tabella `enterprise`.
- **Nota:** Per trovare il nome, la posizione geografica (`geometry`, `town`, `country`) o la Partita IVA di un edificio, devi consultare il record `enterprise` con lo stesso identico `id`.

## Query di Esempio

Recupera i dettagli completi di un edificio unendo i suoi dati strutturali specifici con i dati generali dell'impresa (come nome e città):

```sql
SELECT
    e.name,
    e.town,
    b.n_floors,
    b.construction_cost,
    b.economic_value
FROM
    building b
JOIN
    enterprise e ON b.id = e.id
WHERE
    e.type = 'BUILDING';
```