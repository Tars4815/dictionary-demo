# Table: `damage_church_structure`

**Description (EN):** This table represents structural damages to church structures. In the database's inheritance architecture, it acts as a direct sub-type of the [`damage`](damage.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `damage` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the damage to church structures| `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `damage.id` |
| `variant` | VARCHAR | [...] | [...] | - | No | [...]|
| `scale` | VARCHAR | [...] | [...] | - | No | [...]|
| `extension_percent` | BIGINT | [...] | [...] | - | No | [...]|
| `damage_to_foundations` | BOOLEAN | [...] | [...] | - | No | [...]|

## Relationships

* **Inherits from (Sub-type of):** [`damage`](damage.md). The `damage_church_structure` table is a specialized extension of the `damage` table.
* **Affects:** [`component`](component.md) (One or more damages affect a component or its subclasses)
* **Is reported by:** [`survey`](survey.md) (One or more damages is reported in a survey)
* **Reported in:** [`attachment`](attachment.md) (A damage is reported in one or more attachments)
* **Results in:** [`economic_loss`](economic_loss.md)

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or other details of a damage to church structures, you must join this table with the `damage` record that shares the exact same `id`.

## Example Query

Retrieve a list of all damages to goods, including their descriptions, towns, and spatial coordinates, by joining the table with its parent `damage` entity:

```sql
SELECT
    dcs.*,
    d.*
FROM 
    damage_church_structure dcs   join damage d on dcs.id = d.id
```