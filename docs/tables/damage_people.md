# Table: `damage_people`

**Description (EN):** This table represents damages reported to people. In the database's inheritance architecture, it acts as a direct sub-type of the [`damage`](damage.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `damage` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for damages to people | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `damage.id` |
| `number_of_dead` | INTEGER | [...] | [...] | - | No | - |
| `number_of_injured` | INTEGER | [...] | [...] | - | No | - |
| `number_of_missing` | INTEGER | [...] | [...] | - | No | - |

## Relationships

* **Inherits from (Sub-type of):** [`damage`](damage.md). The `damage_people` table is a specialized extension of the `damage` table.

[...]