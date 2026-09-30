# Table: `livestock`

**Description (EN):** This table represents livestock components. In the database's inheritance architecture, it acts as a direct sub-type of the [`component`](component.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `component` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the livestock | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `component.id` |
| `age` | BIGINT | [...] | `2` | - | No | - |
| `breeding_cost` | BIGINT | [...] | `2` | - | No | - |
| `gate_price` | BIGINT | [...] | `2` | - | No | - |
| `weight` | BIGINT | [...] | `2` | - | No | - |
| `year_production` | BIGINT | [...] | `2` | - | No | - |
| `subtype` | VARCHAR | [...] | - | - | No | - |
| `purpose` | VARCHAR | [...] | - | - | No | - |

## Relationships

* **Inherits from (Sub-type of):** [`component`](component.md). The `livestock` table is a specialized extension of the `component` table.
* **Belongs to:** [`enterprise`](enterprise.md) (A component sub-type is linked to one enterprise)
* **Has many:** `damage` (A component sub-type can be affected by multiple damage over time)

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or ownership details of a livestock, you must join this table with the `component` record that shares the exact same `id`.

## Example Query

Retrieve a list of all livestocks, including their names, towns, and spatial coordinates, by joining the table with its parent `component` entity:

```sql
SELECT 
    l.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    livestock l
JOIN 
    component c ON l.id = c.id
WHERE 
    c.component_kind  = 'LIVESTOCK';
```