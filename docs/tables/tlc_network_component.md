# Table: `tlc_network_component`

!!! info "Different name in the web-app (GUI)"
    In the PostgreSQL backend, this table is named `tlc_network_component`, as shown in the page title. In the web-app interface it appears as **Telecom element**. All aliases are listed in the [correspondence table](../backend-to-gui.md).

**Description (EN):** This table represents telecommunication network components. In the database's inheritance architecture, it acts as a direct sub-type of the [`component`](component.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `component` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the telecommunication network component | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `component.id` |
| `value` | BIGINT | [...] | [...] | - | No | - |
| `component` | VARCHAR | [...] | [...] | - | No | - |

## Relationships

* **Inherits from (Sub-type of):** [`component`](component.md). The `tlc_network_component` table is a specialized extension of the `component` table.
* **Belongs to:** [`enterprise`](enterprise.md) (A component sub-type is linked to one enterprise)
* **Has many:** `damage` (A component sub-type can be affected by multiple damage over time)

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or ownership details of a telecommunication network component, you must join this table with the `component` record that shares the exact same `id`.

## Example Query

Retrieve a list of all telecommunication network components, including their names, towns, and spatial coordinates, by joining the table with its parent `component` entity:

```sql
SELECT 
    tnc.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    tlc_network_component tnc 
JOIN 
    component c ON tnc.id = c.id
```