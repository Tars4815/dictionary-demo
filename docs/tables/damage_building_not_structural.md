# Table: `damage_building_not_structural`

**Description (EN):** This table represents non-structural damages to building functionalities. In the database's inheritance architecture, it acts as a direct sub-type of the [`damage`](damage.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `damage` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the non-structural damage to a building | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `damage.id` |
| `non_structural_element` | VARCHAR | [...] | [...] | - | No | [...]|
| `non_structural_damage_type` | VARCHAR | [...] | [...] | - | No | [...]|
| `damage_quantification` | VARCHAR | [...] | [...] | - | No | [...]|

## Relationships

* **Inherits from (Sub-type of):** [`damage`](damage.md). The `damage_building_not_structural` table is a specialized extension of the `damage` table.
* **Affects:** [`component`](component.md) (One or more damages affect a component or its subclasses)
* **Is reported by:** [`survey`](survey.md) (One or more damages is reported in a survey)
* **Reported in:** [`attachment`](attachment.md) (A damage is reported in one or more attachments)
* **Results in:** [`economic_loss`](economic_loss.md)

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or other details of a non-structural damage to buildings, you must join this table with the `damage` record that shares the exact same `id`.

## Example Query

Retrieve a list of all non-structural damages to buildings, including their names, towns, and spatial coordinates, by joining the table with its parent `damage` entity:

```sql
SELECT
    dbns.*,
    d.*
FROM 
    damage_building_not_structural dbns join damage d on dbns.id = d.id
```