# Table: `damage_staff`

**Description (EN):** This table represents damages reported to farm staff. In the database's inheritance architecture, it acts as a direct sub-type of the [`farm_damage`](farm_damage.md) table, which is itself a sub-type of [`damage`](damage.md). It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as description, dates, location and geometry) from its parent `damage` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the damage to farm staff | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `farm_damage.id` (and, in turn, `damage.id`) |
| `duration_of_absence` | INTEGER | [...] | [...] | - | No | - |
| `number_of_absent` | INTEGER | [...] | [...] | - | No | - |
| `number_of_dead` | INTEGER | [...] | [...] | - | No | - |
| `number_of_injured` | INTEGER | [...] | [...] | - | No | - |
| `further_details` | VARCHAR | [...] | [...] | - | No | - |
| `reason_of_absence` | VARCHAR | [...] | [...] | - | No | - |
| `number_of_missing` | INTEGER | [...] | [...] | - | No | - |

## Relationships

* **Inherits from (Sub-type of):** [`farm_damage`](farm_damage.md), which in turn inherits from [`damage`](damage.md). The `damage_staff` table is a specialized extension of the `farm_damage` table.
* **Affects:** [`component`](component.md) (One or more damages affect a component or its subclasses)
* **Is reported by:** [`survey`](survey.md) (One or more damages is reported in a survey)
* **Reported in:** [`attachment`](attachment.md) (A damage is reported in one or more attachments)
* **Results in:** [`economic_loss`](economic_loss.md)

!!! tip "Where is the rest of the data?"
    To find the description, dates, geographical location (`geometry`, `town`, `country`), or other details of a damage to staff, you must join this table with the `damage` record that shares the exact same `id`.

## Example Query

Retrieve a list of all damages to staff, including their descriptions, towns, and spatial coordinates, by joining the table with its parent `damage` entity:

```sql
SELECT
    ds.*,
    d.*
FROM 
    damage_staff ds JOIN damage d ON ds.id = d.id;
```
