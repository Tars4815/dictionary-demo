# Table: `component`

**Description (EN):** This table stores the universal, high-level attributes—such as identification and geographical location for all major physical or business components. Specific types of components (like [added blocks](added_block.md), [artistic goods](artistic_good.md), or other) store their specialized data in separate sub-tables that share the same ID.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the component | `3` | PK | No | Acts as the universal ID across all sub-type tables |
| `insured` | BOOLEAN | [...] | True | - | No | - |
| `enterprise_id` | BIGINT | [...] | True | - | No | Pointing to id of entity [enterprise](enterprise.md) |
| `country` | VARCHAR | [...] | Italy | - | No | - |
| `county` | VARCHAR | [...] | [...] | - | No | - |
| `details` | VARCHAR | [...] | [...] | - | No | - |
| `hamlet` | VARCHAR | [...] | [...] | - | No | - |
| `house_number` | VARCHAR | [...] | [...] | - | No | - |
| `name` | VARCHAR | [...] | [...] | - | No | - |
| `postcode` | VARCHAR | [...] | [...] | - | No | - |
| `road` | VARCHAR | [...] | [...] | - | No | - |
| `state` | VARCHAR | [...] | [...] | - | No | - |
| `town` | VARCHAR | [...] | [...] | - | No | - |
| `geometry` | GEOMETRY | Spatial representation of the component entity | [...] | - | No | - |
| `coordinates_inferred` | BOOLEAN | [...] | [...] | - | No | - |
| `cultural_heritage` | BOOLEAN | [...] | [...] | - | No | - |
| `component_kind` | BOOLEAN | [...] | [...] | - | No | - |