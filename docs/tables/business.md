# Table: `business`

**Description (EN):** This table represents business enterprises. In the database's inheritance architecture, it acts as a direct sub-type of the [`enterprise`](enterprise.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `enterprise` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the business record | `8` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `enterprise.id` |
| `share_capital` | BIGINT | Total monetary value of funds of the company | [...] | - | No | [...] |
| `nace_section` | VARCHAR | Top-level industry classification of the business's primary economic activity, according to the NACE standard | [...] | - | No | [...] |

## Relationships

* **Inherits from (Sub-type of):** [`enterprise`](enterprise.md). The `business` table is a specialized extension of the `enterprise` table.
* **Contains:** While not linked directly via a `business_id`, a network system owns infrastructural assets through the `enterprise_id` column in the `component` table. These components often include specialized sub-types such as:
    * `business_operations`

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or ownership details of a network system, you must join this table with the `enterprise` record that shares the exact same `id`.

## Example Query

Retrieve a list of all business records, including their names, towns, and spatial coordinates, by joining the table with its parent `enterprise` entity:

```sql
SELECT 
    b.id, 
    e.name, 
    e.town, 
    ST_AsText(e.geometry) as coordinates 
FROM 
    business b
JOIN 
    enterprise e ON b.id = e.id
WHERE 
    e.type = 'BUSINESS';
```