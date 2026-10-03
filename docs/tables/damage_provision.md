# Table: `damage_provision`

**Description (EN):** This table represents damages reported to provisions. In the database's inheritance architecture, it acts as a direct sub-type of the [`farm_damage`](farm_damage.md) table, which is itself a sub-type of [`damage`](damage.md). It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as description, dates, location and geometry) from its parent `damage` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the damage to provisions | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `farm_damage.id` (and, in turn, `damage.id`) |
| `additional_food` | INTEGER | [...] | [...] | - | No | - |
| `additional_veterinary` | INTEGER | [...] | [...] | - | No | - |
| `losses_fees` | INTEGER | [...] | [...] | - | No | - |
| `losses_premature_sale` | INTEGER | [...] | [...] | - | No | - |
| `losses_value` | INTEGER | [...] | [...] | - | No | - |
| `relocation_cost` | INTEGER | [...] | [...] | - | No | - |
| `replanting_cost` | INTEGER | [...] | [...] | - | No | - |
| `additional_materials` | INTEGER | [...] | [...] | - | No | - |
| `restoration_cost` | INTEGER | [...] | [...] | - | No | - |

## Relationships

* **Inherits from (Sub-type of):** [`farm_damage`](farm_damage.md), which in turn inherits from [`damage`](damage.md). The `damage_provision` table is a specialized extension of the `farm_damage` table.
* **Affects:** [`component`](component.md) (One or more damages affect a component or its subclasses)
* **Is reported by:** [`survey`](survey.md) (One or more damages is reported in a survey)
* **Reported in:** [`attachment`](attachment.md) (A damage is reported in one or more attachments)
* **Results in:** [`economic_loss`](economic_loss.md)

!!! tip "Where is the rest of the data?"
    To find the description, dates, geographical location (`geometry`, `town`, `country`), or other details of a damage to provisions, you must join this table with the `damage` record that shares the exact same `id`.

## Example Query

Retrieve a list of all damages to provisions, including their descriptions, towns, and spatial coordinates, by joining the table with its parent `damage` entity:

```sql
SELECT
    dp.*,
    d.*
FROM 
    damage_provision dp JOIN damage d ON dp.id = d.id;
```
