# Table: `farm_damage`

**Description (EN):** This table represents damages reported to farms. In the database's inheritance architecture, it acts as a direct sub-type of the [`damage`](damage.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as description, dates, location and geometry) from its parent `damage` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the damage to a farm | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `damage.id` |

## Relationships

* **Inherits from (Sub-type of):** [`damage`](damage.md). The `farm_damage` table is a specialized extension of the `damage` table.
* **Affects:** [`component`](component.md) (One or more damages affect a component or its subclasses)
* **Is reported by:** [`survey`](survey.md) (One or more damages is reported in a survey)
* **Reported in:** [`attachment`](attachment.md) (A damage is reported in one or more attachments)
* **Results in:** [`economic_loss`](economic_loss.md)
* **Has Sub-types (Inheritance):** The following tables inherit from `farm_damage` and share its `id`:
    * [`damage_agriculture_product`](damage_agriculture_product.md)
    * [`damage_fixed_asset`](damage_fixed_asset.md)
    * [`damage_livestock`](damage_livestock.md)
    * [`damage_provision`](damage_provision.md)
    * [`damage_staff`](damage_staff.md)

!!! tip "Where is the rest of the data?"
    To find the description, dates, geographical location (`geometry`, `town`, `country`), or other details of a damage to farms, you must join this table with the `damage` record that shares the exact same `id`.

## Example Query

Retrieve a list of all damages to farms, including their descriptions, towns, and spatial coordinates, by joining the table with its parent `damage` entity:

```sql
SELECT
    fd.*,
    d.*
FROM 
    farm_damage fd JOIN damage d ON fd.id = d.id;
```
