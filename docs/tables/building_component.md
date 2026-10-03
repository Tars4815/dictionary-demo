# Table: `building_component`

**Description (EN):** This table stores the structural, economic and physical characteristics of buildings, including construction details, material types and dimensions. In the database's inheritance architecture, it acts as a direct sub-type of the [`component`](component.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location and geometry) from its parent `component` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the building component | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `component.id` |
| `principal` | BOOLEAN | [...] | `true` | - | No | [...] |
| `subtype` | VARCHAR(255) | [...] | [...] | - | No | [...] |
| `public_service_code` | VARCHAR(255) | [...] | [...] | - | No | [...] |
| `heritage_tier` | VARCHAR(255) | [...] | [...] | - | No | [...] |
| `year` | INTEGER | Construction year | `1999` | - | No | |
| `quality` | VARCHAR(255) | Overall quality | `GOOD` | - | No | Possible values: POOR, GOOD, ACCEPTABLE, NOT_IDENTIFIABLE |
| `conservation` | VARCHAR(255) | Conservation status of the building | `POORLY_MANTAINED` | CHECK | No | Possible values: POORLY_MANTAINED, MODERATELY_MAINTAINED, WELL_MAINTAINED, NOT_IDENTIFIABLE |
| `retrofitting` | VARCHAR(255) | Status of retrofitting | `NOT_IDENTIFIABLE` | CHECK | No | Possible values: NONE, VERTICAL, HORIZONTAL, COMPLETE, NOT_IDENTIFIABLE, etc |
| `regularity` | VARCHAR(255) | Regularity of structure | `NOT_IDENTIFIABLE` | CHECK | No | Possible values: NOT_REGULAR, COMPLETELY_REGULAR, etc |
| `inhabitants` | INTEGER | Number of inhabitants of the given building | `6` | - | No | |
| `construction_cost` | INTEGER | Construction cost | `500000` | - | No | |
| `economic_value` | INTEGER | Economic value | `1000000` | - | No | |
| `vertical_mat` | VARCHAR(255) | Construction material of the vertical structures | `NOT_IDENTIFIABLE` | CHECK | No | Possible values: STEEL, WOOD, MASONRY_ADOBE, etc |
| `horizontal_mat` | VARCHAR(255) | Construction material of the horizontal structures | `MASONRY_ADOBE` | CHECK | No | Possible values: STEEL, WOOD, MASONRY_ADOBE, etc |
| `roof_mat` | VARCHAR(255) | Material of the roof element | `NOT_IDENTIFIABLE` | CHECK | No | Possible values: STEEL, WOOD, MASONRY_ADOBE, etc |
| `build_position` | VARCHAR(255) | Building position | `SINGLE_DETACHED` | CHECK | No | Possible values: SINGLE_DETACHED, SEMI_DETACHED, ROW, NOT_IDENTIFICABLE |
| `ground_floor` | VARCHAR(255) | Typology of ground floor | `OPEN` | CHECK | No | Possible values: OPEN, CLOSE, NOT_IDENTIFIABLE |
| `n_floors` | INTEGER | Number of floors above the ground | `3` | - | No | |
| `floor_height` | INTEGER | Average height of floors | `4` | - | No | |
| `n_under_floors` | INTEGER | Number of underground floors | `1` | - | No | |
| `floor_area` | INTEGER | Metric surface of the floor area | `1000` | - | No | |
| `usage` | VARCHAR(255) | [...] | [...] | - | No | [...] |
| `foundation_typology` | VARCHAR(255) | [...] | [...] | - | No | [...] |
| `main_use` | VARCHAR(255) | [...] | [...] | - | No | [...] |

## Relationships

* **Inherits from (Sub-type of):** [`component`](component.md). The `building_component` table is a specialized extension of the `component` table.
* **Belongs to:** [`enterprise`](enterprise.md) (A component sub-type is linked to one enterprise)
* **Has many:** `damage` (A component sub-type can be affected by multiple damage over time)

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or ownership details of a building component, you must join this table with the `component` record that shares the exact same `id`.

## Example Query

Retrieve a list of all building components, including their names, towns, and spatial coordinates, by joining the table with its parent `component` entity:

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
