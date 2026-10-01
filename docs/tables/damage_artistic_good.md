# Table: `damage_artistic_good`

**Description (EN):** This table represents damages to artistic goods. In the database's inheritance architecture, it acts as a direct sub-type of the [`damage`](damage.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `damage` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the damage to artistic goods| `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `damage.id` |
| `kind` | VARCHAR | [...] | [...] | - | No | [...]|
| `level` | VARCHAR | [...] | [...] | - | No | [...]|
| `extension_percent` | BIGINT | [...] | [...] | - | No | [...]|


## Relationships

* **Inherits from (Sub-type of):** [`damage`](damage.md). The `damage_artistic_good` table is a specialized extension of the `damage` table.
* **Affects:** [`component`](component.md) (One or more damages affect a component or its subclasses)
* **Is reported by:** [`survey`](survey.md) (One or more damages is reported in a survey)
* **Reported in:** [`attachment`](attachment.md) (A damage is reported in one or more attachments)
* **Results in:** [`economic_loss`](economic_loss.md)

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or other details of a damage to artistic good, you must join this table with the `damage` record that shares the exact same `id`.

## Example Query

Retrieve a list of all damages to artistic goods, including their names, towns, and spatial coordinates, by joining the table with its parent `damage` entity:

```sql
SELECT
    dag.*,
    d.*
FROM 
    damage_artistic_good dag join damage d on dag.id = d.id
```