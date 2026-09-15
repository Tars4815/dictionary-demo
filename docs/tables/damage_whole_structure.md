# Table: `damage_whole_structure`

**Description (EN):** This table represents damages reported to whole structures. In the database's inheritance architecture, it acts as a direct sub-type of the [`damage`](damage.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `damage` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the whole structure damage | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `damage.id` |
| `scale` | VARCHAR | [...] | [...] | - | No | - |
| `extension_percent` | INTEGER | [...] | [...] | - | No | - |

## Relationships

* **Inherits from (Sub-type of):** [`damage`](damage.md). The `damage_whole_structure` table is a specialized extension of the `damage` table.

[...]