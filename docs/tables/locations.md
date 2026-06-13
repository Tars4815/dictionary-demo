# Tabella: `locations`

**Descrizione:** Questa tabella memorizza i punti di interesse geografici e i relativi metadati.

## Struttura Colonne

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | UUID | Identificativo univoco | `123e4567...` | PK | No | Generato automaticamente |
| `name` | VARCHAR(255) | Nome del luogo | `Piazza Roma` | NOT NULL | No | |
| `geom` | POINT | Coordinate spaziali | `POINT(12 41)` | | Sì | Sistema EPSG:4326 |
| `user_id` | UUID | Creatore del record | `987f6543...` | FK | No | Rif. a `users.id` |

## Relazioni
* **Appartiene a:** [`users`](users.md) (tramite `user_id`)
* **Ha molti:** `events` (tramite `location_id`)

## Query di Esempio (Opzionale)
```sql
SELECT name, ST_AsText(geom) FROM locations WHERE user_id = '...';