# Table: `damage_product`

**Description (EN):** This table represents damages to products. In the database's inheritance architecture, it acts as a direct sub-type of the [`damage`](damage.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `damage` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for damages to products | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `damage.id` |
| `quality_loss_percentage` | INTEGER | [...] | [...] | - | No | - |
| `manufacturing_loss_percentage` | INTEGER | [...] | [...] | - | No | - |
| `total_damage_percentage` | INTEGER | [...] | [...] | - | No | - |
| `non_produced_good_quantity` | INTEGER | [...] | [...] | - | No | - |
| `non_transformed_good_quantity` | INTEGER | [...] | [...] | - | No | - |

## Relationships

* **Inherits from (Sub-type of):** [`damage`](damage.md). The `damage_product` table is a specialized extension of the `damage` table.
* **Affects:** [`component`](component.md) (One or more damages affect a component or its subclasses)
* **Is reported by:** [`survey`](survey.md) (One or more damages is reported in a survey)
* **Reported in:** [`attachment`](attachment.md) (A damage is reported in one or more attachments)
* **Results in:** [`economic_loss`](economic_loss.md)

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or other details of a damage to products, you must join this table with the `damage` record that shares the exact same `id`.

## Example Query

Retrieve a list of all damages to products, including their descriptions, towns, and spatial coordinates, by joining the table with its parent `damage` entity:

```sql
SELECT
    dp.*,
    d.*
FROM 
    damage_product dp  join damage d on dp.id = d.id
```