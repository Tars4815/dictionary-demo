# Table: `building`

**Description (EN):** This table represents buildings. In the database's inheritance architecture, it acts as a direct sub-type of the [`enterprise`](enterprise.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `enterprise` record.

The structural, economic and physical characteristics of a building (construction year, materials, number of floors, cost, and so on) are stored in the [`building_component`](building_component.md) table.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Building unique identifier | `3` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `enterprise.id` |

## Relationships

* **Inherits from (Sub-type of):** [`enterprise`](enterprise.md). The `building` table is a specialized extension of the `enterprise` table.
* **Contains:** While not linked directly via a `building_id`, a building owns its physical parts through the `enterprise_id` column in the `component` table. These components often include specialized sub-types such as:
    * [`building_component`](building_component.md)
    * [`added_block`](added_block.md)
    * [`building_functionality`](building_functionality.md)

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or VAT of a building, you must join this table with the `enterprise` record that shares the exact same `id`. The structural and economic characteristics are in `building_component`, which is linked to the building through `component.enterprise_id`.

## Example Query

Retrieve the characteristics of each building by joining its enterprise record with its building components:

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
