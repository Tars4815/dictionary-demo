# Table: `staff`

**Description (EN):** This table represents staff components. In the database's inheritance architecture, it acts as a direct sub-type of the [`component`](component.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `component` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the staff component | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `component.id` |
| `number` | BIGINT | [...] | [...] | - | No | - |
| `activities` | VARCHAR | [...] | [...] | - | No | - |
| `staff_category` | VARCHAR | [...] | [...] | - | No | - |

## Relationships

* **Inherits from (Sub-type of):** [`component`](component.md). The `staff` table is a specialized extension of the `component` table.
* **Belongs to:** [`enterprise`](enterprise.md) (A component sub-type is linked to one enterprise)
* **Has many:** `damage` (A component sub-type can be affected by multiple damage over time)

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or ownership details of a staff, you must join this table with the `component` record that shares the exact same `id`.

## Example Query

Retrieve a list of all staff records, including their names, towns, and spatial coordinates, by joining the table with its parent `component` entity:

```sql
SELECT 
    s.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    staff s 
JOIN 
    component c ON s.id = c.id
```