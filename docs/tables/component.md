# Table: `component`

**Description (EN):** This table stores the universal, high-level attributes, such as identification and geographical location, for all major physical or business components. Specific types of components (like [added blocks](added_block.md), [artistic goods](artistic_good.md), or other) store their specialized data in separate sub-tables that share the same ID.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the component | `3` | PK | No | Acts as the universal ID across all sub-type tables |
| `component_kind` | VARCHAR | Discriminator column identifying the specific sub-type of the component | `BUILDING_COMPONENT` | NOT NULL | No | Holds the most specific type. Values currently present in the data: 'BUILDING_COMPONENT', 'TRANSPORT_COMPONENT', 'TRANSPORT_SERVICE', 'ADDED_BLOCK', 'CROP' |
| `enterprise_id` | BIGINT | Identifier of the enterprise the component belongs to | `42` | FK | No | Pointing to id of entity [enterprise](enterprise.md) |
| `insured` | BOOLEAN | [...] | `True` | - | No | - |
| `name` | VARCHAR | [...] | [...] | - | No | - |
| `country` | VARCHAR | [...] | `Italy` | - | No | - |
| `state` | VARCHAR | [...] | [...] | - | No | - |
| `county` | VARCHAR | [...] | [...] | - | No | - |
| `town` | VARCHAR | [...] | [...] | - | No | - |
| `hamlet` | VARCHAR | [...] | [...] | - | No | - |
| `road` | VARCHAR | [...] | [...] | - | No | - |
| `house_number` | VARCHAR | [...] | [...] | - | No | - |
| `postcode` | VARCHAR | [...] | [...] | - | No | - |
| `details` | VARCHAR | [...] | [...] | - | No | - |
| `geometry` | GEOMETRY | Spatial representation of the component entity | [...] | - | Yes | - |
| `coordinates_inferred` | BOOLEAN | [...] | [...] | - | No | - |
| `cultural_heritage` | BOOLEAN | [...] | [...] | - | No | - |

## Relationships

Because `component` is one of the core entities of the schema, it has extensive relationships:

* **Has Sub-types (Inheritance):** The following tables inherit from `component` and share its `id`:
    * [`added_block`](added_block.md)
    * [`artistic_good`](artistic_good.md)
    * [`agriculture_product`](agriculture_product.md), which has its own sub-types [`crop`](crop.md) and [`stored`](stored.md)
    * [`building_component`](building_component.md)
    * [`building_functionality`](building_functionality.md)
    * [`business_operations`](business_operations.md)
    * [`electrical_network_component`](electrical_network_component.md)
    * [`fixed_asset`](fixed_asset.md), which has its own sub-types [`infrastructure`](infrastructure.md), [`land`](land.md), [`machinery`](machinery.md) and [`material`](material.md)
    * [`livestock`](livestock.md)
    * [`network_service`](network_service.md)
    * [`product`](product.md)
    * [`provision`](provision.md)
    * [`staff`](staff.md)
    * [`tlc_network_component`](tlc_network_component.md)
    * [`transport_network_component`](transport_network_component.md)
* **Belongs to:** [`enterprise`](enterprise.md) (A component is linked to one enterprise)
* **Has many:** [`damage`](damage.md) (A component can be affected by multiple damage over time)
