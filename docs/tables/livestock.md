# Table: `livestock`

**Description (EN):** This table represents livestock components. In the database's inheritance architecture, it acts as a direct sub-type of the [`component`](component.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `component` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the livestock | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `component.id` |
| `age` | BIGINT | [...] | `2` | - | No | - |
| `breeding_cost` | BIGINT | [...] | `2` | - | No | - |
| `gate_price` | BIGINT | [...] | `2` | - | No | - |
| `weight` | BIGINT | [...] | `2` | - | No | - |
| `year_production` | BIGINT | [...] | `2` | - | No | - |
| `subtype` | VARCHAR | [...] | - | - | No | - |
| `purpose` | VARCHAR | [...] | - | - | No | - |

[...]