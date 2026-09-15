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

## Relationships

Because `component` is one of the core entities of the schema, it has extensive relationships:

* **Has Sub-types (Inheritance):** The following tables inherit from `component` and share its `id`:
    * [`added block`](added_block.md)
    * [`artistic good`](artistic_good.md)
    * [`building component`](building_component.md)
    * [`building functionality`](building_functionality.md)
    * [`electrical network component`](electrical_network_component.md)
    * [`livestock`](livestock.md)
    * [`network service`](network_service.md)
    * [`provision`](provision.md)
    * [`staff`](staff.md)
* **Belongs to:** [`enterprise`](enterprise.md) (A component is linked to one enterprise)
* **Has many:** `damage` (A component can be affected by multiple damage over time)