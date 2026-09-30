# Table: `tlc_system`

**Description (EN):** This table represents telecommunications network systems. In the database's inheritance architecture, it acts as a direct sub-type of the [`network_system`](network_system.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `network_system`, which on turn is a child of a [`enterprise`](enterprise.md) record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the telecommunication network system | `8` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `network_system.id` and `enterprise.id` |

## Relationships

* **Inherits from (Sub-type of):** [`network_system`](network_system.md). The `tlc_system` table is a specialized extension of the `network_system` table.
* **Contains:** While not linked directly via a `tlc_system_id`, a telecommunication system owns infrastructural assets through the `enterprise_id` column in the `component` table. These components often include specialized sub-types such as:
    * `tlc_network_component`

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or ownership details of a network system, you must join this table with the `enterprise` record that shares the exact same `id`.

## Example Query

Retrieve a list of all electrical systems, including their names, towns, and spatial coordinates, by joining the table with its parent `network_system` - `enterprise` entity:

```sql
SELECT 
    tlc.id, 
    e.name, 
    e.town, 
    ST_AsText(e.geometry) as coordinates 
FROM 
    tlc_system tlc
JOIN 
    enterprise e ON tlc.id = e.id
WHERE 
    e.type = 'TLC_SYSTEM';