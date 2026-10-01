# Table: `network_service`

**Description (EN):** This table represents business products. In the database's inheritance architecture, it acts as a direct sub-type of the [`component`](component.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `component` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for business product | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `component.id` |
| `product_kind` | VARCHAR | [...] | [...] | - | No | - |
| `category` | VARCHAR | [...] | [...] | - | No | - |
| `quantity` | BIGINT | [...] | [...] | - | No | - |
| `unit` | VARCHAR | [...] | [...] | - | No | - |
| `value` | BIGINT | [...] | [...] | - | No | - |

## Relationships

* **Inherits from (Sub-type of):** [`component`](component.md). The `product` table is a specialized extension of the `component` table.
* **Belongs to:** [`enterprise`](enterprise.md) (A component sub-type is linked to one enterprise)
* **Has many:** `damage` (A component sub-type can be affected by multiple damage over time)

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or ownership details of a product, you must join this table with the `component` record that shares the exact same `id`.

## Example Query

Retrieve a list of all products, including their names, towns, and spatial coordinates, by joining the table with its parent `component` entity:

```sql
SELECT 
    p.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    product p 
JOIN 
    component c ON p.id = c.id
```