# Table: `damage_building_functionality`

**Description (EN):** This table represents damages to building functionalities. In the database's inheritance architecture, it acts as a direct sub-type of the [`damage`](damage.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `damage` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the damage to a building functionality| `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `damage.id` |
| `floor_number` | BIGINT | [...] | [...] | - | No | [...]|
| `loss_of_service` | BIGINT | [...] | [...] | - | No | [...]|
| `temporary_description` | VARCHAR | [...] | [...] | - | No | [...]|
| `temporary` | VARCHAR | [...] | [...] | - | No | [...]|
| `outage` | VARCHAR | [...] | [...] | - | No | [...]|
| `subtype` | VARCHAR | [...] | [...] | - | No | [...]|
| `apartment_code` | VARCHAR | [...] | [...] | - | No | [...]|

## Relationships

* **Inherits from (Sub-type of):** [`damage`](damage.md). The `damage_building_functionality` table is a specialized extension of the `damage` table.
* **Affects:** [`component`](component.md) (One or more damages affect a component or its subclasses)
* **Is reported by:** [`survey`](survey.md) (One or more damages is reported in a survey)
* **Reported in:** [`attachment`](attachment.md) (A damage is reported in one or more attachments)
* **Results in:** [`economic_loss`](economic_loss.md)

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or other details of a damage to building functionalities, you must join this table with the `damage` record that shares the exact same `id`.

## Example Query

Retrieve a list of all damages to building functionalities, including their names, towns, and spatial coordinates, by joining the table with its parent `damage` entity:

```sql
SELECT
    dbf.*,
    d.*
FROM 
    damage_building_functionality dbf join damage d on dbf.id = d.id
```