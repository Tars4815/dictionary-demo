# Table: `component`

**Description (EN):** This table stores the universal, high-level attributes, such as identification and geographical location, for all major physical or business components. Specific types of components (like [added blocks](added_block.md), [artistic goods](artistic_good.md), or other) store their specialized data in separate sub-tables that share the same ID.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the component | `3` | PK | No | Acts as the universal ID across all sub-type tables |
| `component_kind` | VARCHAR | Discriminator column identifying the specific sub-type of the component | `BUILDING_COMPONENT` | NOT NULL | No | Holds the most specific type. Values currently present in the data: 'BUILDING_COMPONENT', 'TRANSPORT_COMPONENT', 'TRANSPORT_SERVICE', 'ADDED_BLOCK', 'CROP' |
| `enterprise_id` | BIGINT | Identifier of the enterprise the component belongs to | `42` | FK | No | Pointing to id of entity [enterprise](enterprise.md) |
| `insured` | BOOLEAN | Whether the component is covered by insurance | `True` | - | No | - |
| `name` | VARCHAR | Name or denomination of the component | `Warehouse A` | - | No | - |
| `country` | VARCHAR | Country where the component is located | `Italy` | - | No | - |
| `state` | VARCHAR | State or region where the component is located | `Lazio` | - | No | - |
| `county` | VARCHAR | County or province where the component is located | `Rome` | - | No | - |
| `town` | VARCHAR | Municipality where the component is located | `Rome` | - | No | - |
| `hamlet` | VARCHAR | Hamlet or locality where the component is located | `Trastevere` | - | No | - |
| `road` | VARCHAR | Street where the component is located | `Via Appia` | - | No | - |
| `house_number` | VARCHAR | House number of the component | `10` | - | No | - |
| `postcode` | VARCHAR | Postal code of the component | `00100` | - | No | - |
| `details` | VARCHAR | Additional address details of the component | `Building B, second floor` | - | No | - |
| `geometry` | GEOMETRY | Spatial representation of the component entity | [...] | - | Yes | - |
| `coordinates_inferred` | BOOLEAN | Whether the coordinates of the component were inferred rather than directly measured | [...] | - | No | - |
| `cultural_heritage` | BOOLEAN | Whether the component is a cultural heritage asset | [...] | - | No | - |

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
