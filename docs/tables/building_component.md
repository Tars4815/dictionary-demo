# Table: `building_component`

**Description (EN):** This table represents building components. In the database's inheritance architecture, it acts as a direct sub-type of the [`component`](component.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `component` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the building component | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `component.id` |
| `principal` | BOOLEAN | [...] | `true` | - | No | [...] |
| `subtype` | VARCHAR | [...] | [...] | - | No | [...] |
| `public_service_code` | VARCHAR | [...] | [...] | - | No | [...] |
| `heritage_tier` | VARCHAR | [...] | [...] | - | No | [...] |
| `year` | BIGINT | [...] | [...] | - | No | [...] |
| `quality` | VARCHAR | [...] | [...] | - | No | [...] |
| `conservation` | VARCHAR | [...] | [...] | - | No | [...] |
| `retrofitting` | VARCHAR | [...] | [...] | - | No | [...] |
| `regularity` | VARCHAR | [...] | [...] | - | No | [...] |
| `inhabitants` | BIGINT | [...] | [...] | - | No | [...] |
| `construction_cost` | BIGINT | [...] | [...] | - | No | [...] |
| `economic_value` | BIGINT | [...] | [...] | - | No | [...] |
| `vertical_mat` | VARCHAR | [...] | [...] | - | No | [...] |
| `horizontal_mat` | VARCHAR | [...] | [...] | - | No | [...] |
| `roof_mat` | VARCHAR | [...] | [...] | - | No | [...] |
| `build_position` | VARCHAR | [...] | [...] | - | No | [...] |
| `ground_floor` | VARCHAR | [...] | [...] | - | No | [...] |
| `n_floors` | BIGINT | [...] | [...] | - | No | [...] |
| `floor_heights` | BIGINT | [...] | [...] | - | No | [...] |
| `n_under_floors` | BIGINT | [...] | [...] | - | No | [...] |
| `floor_area` | BIGINT | [...] | [...] | - | No | [...] |
| `usage` | VARCHAR | [...] | [...] | - | No | [...] |
| `foundation_typology` | VARCHAR | [...] | [...] | - | No | [...] |
| `main_use` | VARCHAR | [...] | [...] | - | No | [...] |

## Relationships

* **Inherits from (Sub-type of):** [`component`](component.md). The `building_component` table is a specialized extension of the `component` table.
* **Belongs to:** [`enterprise`](enterprise.md) (A component sub-type is linked to one enterprise)
* **Has many:** `damage` (A component sub-type can be affected by multiple damage over time)

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or ownership details of a building component, you must join this table with the `component` record that shares the exact same `id`.

## Example Query

Retrieve a list of all building components, including their names, towns, and spatial coordinates, by joining the table with its parent `enterprise` entity:

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
    c.component_kind  = 'BUILDING_COMPONENT';
```