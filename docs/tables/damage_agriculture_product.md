# Table: `damage_agriculture_product`

**Description (EN):** This table represents damages reported to agriculture products. In the database's inheritance architecture, it acts as a direct sub-type of the [`farm_damage`](farm_damage.md) table, which is itself a sub-type of [`damage`](damage.md). It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as description, dates, location and geometry) from its parent `damage` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the damage to an agriculture product | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `farm_damage.id` (and, in turn, `damage.id`) |
| `non_produced_good_quantity` | DOUBLE PRECISION | Quantity of goods not produced because of the damage | [...] | - | No | - |
| `quality_loss_percentage` | DOUBLE PRECISION | Percentage of quality loss of the product | [...] | - | No | - |
| `total_damage_percentage` | DOUBLE PRECISION | Total percentage of damage to the product | [...] | - | No | - |
| `total_losses_percentage` | DOUBLE PRECISION | Total percentage of losses | [...] | - | No | - |
| `yield_loss_percentage` | DOUBLE PRECISION | Percentage of yield loss | [...] | - | No | - |

## Relationships

* **Inherits from (Sub-type of):** [`farm_damage`](farm_damage.md), which in turn inherits from [`damage`](damage.md). The `damage_agriculture_product` table is a specialized extension of the `farm_damage` table.
* **Affects:** [`component`](component.md) (One or more damages affect a component or its subclasses)
* **Is reported by:** [`survey`](survey.md) (One or more damages is reported in a survey)
* **Reported in:** [`attachment`](attachment.md) (A damage is reported in one or more attachments)
* **Results in:** [`economic_loss`](economic_loss.md)

!!! tip "Where is the rest of the data?"
    To find the description, dates, geographical location (`geometry`, `town`, `country`), or other details of a damage to agriculture products, you must join this table with the `damage` record that shares the exact same `id`.

## Example Query

Retrieve a list of all damages to agriculture products, including their descriptions, towns, and spatial coordinates, by joining the table with its parent `damage` entity:

```sql
SELECT
    dap.*,
    d.*
FROM 
    damage_agriculture_product dap JOIN damage d ON dap.id = d.id;
```
