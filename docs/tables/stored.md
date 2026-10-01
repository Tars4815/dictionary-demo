# Table: `stored`

**Description (EN):** This table represents stored. In the database's inheritance architecture, it acts as a direct sub-type of the [`agriculture_product`](agriculture_product.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `component` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for stored agriculture products | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `agriculture_product.id` and on turn `component.id` |
| `total_stored` | BIGINT | [...] | [...] | - | No | [...] |

## Relationships

* **Inherits from (Sub-type of):** [`agriculture_product`](agriculture_product.md). The `crop` table is a specialized extension of the `agriculture_product` table.
* **Belongs to:** [`enterprise`](enterprise.md) (A component sub-type is linked to one enterprise)
* **Has many:** `damage` (A component sub-type can be affected by multiple damage over time)

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or ownership details of a stored product, you must join this table with the `component` record that shares the exact same `id`.

## Example Query

Retrieve a list of all stored records, including their names, towns, and spatial coordinates, by joining the table with its parent `enterprise` entity:

```sql
SELECT s.* FROM public."stored" AS s
```