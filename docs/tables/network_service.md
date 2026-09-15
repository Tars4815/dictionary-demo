# Table: `network_service`

**Description (EN):** This table represents network service components. In the database's inheritance architecture, it acts as a direct sub-type of the [`component`](component.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `component` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the network service component | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `component.id` |
| `value` | BIGINT | [...] | [...] | - | No | - |
| `service` | VARCHAR | [...] | [...] | - | No | - |
| `service_user` | VARCHAR | [...] | [...] | - | No | - |

[...]