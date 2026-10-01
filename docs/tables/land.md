# Table: `land`

**Description (EN):** This table represents land. In the database's inheritance architecture, it acts as a direct sub-type of the [`fixed_asset`](fixed_asset.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `component` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for land records | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `fixed_asset.id` and on turn `component.id` |
| `dimension` | BIGINT | [...] | [...] | - | No | [...] |
| `value` | BIGINT | [...] | [...] | - | No | [...] |
| `soil` | VARCHAR | [...] | [...] | - | No | [...] |
| `configuration` | VARCHAR | [...] | [...] | - | No | [...] |
| `function` | VARCHAR | [...] | [...] | - | No | [...] |

## Relationships

* **Inherits from (Sub-type of):** [`fixed_asset`](fixed_asset.md). The `land` table is a specialized extension of the `fixed_asset` table.
* **Belongs to:** [`enterprise`](enterprise.md) (A component sub-type is linked to one enterprise)
* **Has many:** `damage` (A component sub-type can be affected by multiple damage over time)

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or ownership details of a land record, you must join this table with the `component` record that shares the exact same `id`.

## Example Query

Retrieve a list of all lands, including their names, towns, and spatial coordinates, by joining the table with its parent `component` entity:

```sql
SELECT l.* FROM public.land AS l
```