# Table: `farm`

**Description (EN):** This table represents agricultural enterprises. In the database's inheritance architecture, it acts as a direct sub-type of the [`enterprise`](enterprise.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `enterprise` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the farm | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `enterprise.id` |

## Relationships

* **Inherits from (Sub-type of):** [`enterprise`](enterprise.md). The `farm` table is a specialized extension of the `enterprise` table.
* **Contains:** While not linked directly via a `farm_id`, a farm owns agricultural assets through the `enterprise_id` column in the `component` table. These components often include specialized agricultural sub-types such as:
    * `crop`
    * `livestock`
    * `agriculture_product`
    * `structure` (e.g., barns, greenhouses)
    * `machinery` (e.g., tractors)

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or ownership details of a farm, you must join this table with the `enterprise` record that shares the exact same `id`.

## Example Query

Retrieve a list of all farms, including their names, towns, and spatial coordinates, by joining the table with its parent `enterprise` entity:

```sql
SELECT 
    f.id, 
    e.name, 
    e.town, 
    ST_AsText(e.geometry) as coordinates 
FROM 
    farm f
JOIN 
    enterprise e ON f.id = e.id
WHERE 
    e.type = 'FARM';
```