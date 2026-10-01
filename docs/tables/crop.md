# Table: `crop`

**Description (EN):** This table represents crops. In the database's inheritance architecture, it acts as a direct sub-type of the [`agriculture_product`](agriculture_product.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `component` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for crop record | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `agriculture_product.id` and on turn `component.id` |
| `area_planted` | BIGINT | [...] | [...] | - | No | [...] |
| `category` | VARCHAR | [...] | [...] | - | No | [...] |
| `growth` | VARCHAR | [...] | [...] | - | No | [...] |
| `duration` | VARCHAR | [...] | [...] | - | No | [...] |

## Relationships

* **Inherits from (Sub-type of):** [`agriculture_product`](agriculture_product.md). The `crop` table is a specialized extension of the `agriculture_product` table.
* **Belongs to:** [`enterprise`](enterprise.md) (A component sub-type is linked to one enterprise)
* **Has many:** `damage` (A component sub-type can be affected by multiple damage over time)

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or ownership details of a crop, you must join this table with the `component` record that shares the exact same `id`.

## Example Query

Retrieve a list of all crop, including their names, towns, and spatial coordinates, by joining the table with its parent `component` entity:

```sql
SELECT
    c.id,
    c.area_planted,
    c.category,
    ap.year_production 
FROM 
    crop c join agriculture_product ap on c.id = ap.id 
where ap.subtype = 'CROP'
```