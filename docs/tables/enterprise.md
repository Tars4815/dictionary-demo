# Table: `enterprise`

**Description (EN):** This is the core parent entity (superclass) of the database. It stores the universal, high-level attributes, such as identification, geographical location and administrative details, for all major physical or business assets. Specific types of enterprises (like [buildings](building.md), [businesses](business.md), [farms](farm.md) or [network systems](network_system.md)) store their specialized data in separate sub-tables that share the same ID. Ownership is not stored here: it is recorded in the bridge table [`enterprise_owner`](enterprise_owner.md).

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the enterprise | `3` | PK | No | Acts as the universal ID across all sub-type tables |
| `type` | VARCHAR(255) | Discriminator column defining the specific type of enterprise | `BUILDING` | NOT NULL | No | Values currently present in the data: 'BUILDING', 'FARM', 'TRANSPORT', 'TELECOMMUNICATION' |
| `name` | VARCHAR(255) | Official name or denomination of the enterprise | `Main Headquarters` | | No | |
| `management_type` | VARCHAR(255) | Type of management or business administration | `PUBLIC` | | No | e.g., 'PUBLIC', 'PRIVATE', 'MIXED' |
| `vat` | VARCHAR(255) | VAT number of the enterprise | `IT00000000000` | | No | |
| `description` | VARCHAR(255) | Free-text description of the enterprise | `Regional hospital` | | No | |
| `country` | VARCHAR(255) | Country where the enterprise is located | `Italy` | | No | |
| `state` | VARCHAR(255) | State or region where the enterprise is located | `Lazio` | | No | |
| `county` | VARCHAR(255) | County or province where the enterprise is located | `Rome` | | No | |
| `town` | VARCHAR(255) | Municipality where the enterprise is located | `Rome` | | No | |
| `hamlet` | VARCHAR(255) | Hamlet or locality where the enterprise is located | `Trastevere` | | No | |
| `road` | VARCHAR(255) | Street where the enterprise is located | `Via Appia` | | No | |
| `house_number` | VARCHAR(255) | House number of the enterprise | `10` | | No | |
| `postcode` | VARCHAR(255) | Postal code of the enterprise | `00100` | | No | |
| `geometry` | GEOMETRY | Spatial representation of the enterprise | `POINT(12.49 41.89)` | | Yes | EPSG:4326. Can be a Point or a Polygon depending on the scale |
| `coordinates_inferred` | BOOLEAN | Whether the coordinates of the enterprise were inferred rather than directly measured | [...] | | No | |

## Relationships

Because `enterprise` is the central hub of the schema, it has extensive relationships:

* **Has Sub-types (Inheritance):** The following tables inherit from `enterprise` and share its `id`:
    * [`building`](building.md)
    * [`business`](business.md)
    * [`farm`](farm.md)
    * [`network_system`](network_system.md)
* **Is owned by:** [`owner`](owner.md). An enterprise can have several owners, and an owner can hold several enterprises. This many-to-many relationship is mediated by the [`enterprise_owner`](enterprise_owner.md) bridge table.
* **Has many:** [`component`](component.md) (An enterprise is composed of multiple sub-components like machinery, crops, or electrical networks)
* **Has many:** [`survey`](survey.md) (An enterprise can undergo multiple damage or assessment surveys over time)

## Example Query

Retrieve a list of all enterprises located in a specific town, displaying their name, their specific classification (type), and their coordinates:

```sql
SELECT 
    id, 
    name, 
    type, 
    ST_AsText(geometry) as coordinates 
FROM 
    enterprise 
WHERE 
    town = 'Rome'
ORDER BY 
    type ASC;
```

Retrieve the owners of each enterprise through the bridge table:

```sql
SELECT 
    e.id, 
    e.name, 
    o.full_name 
FROM 
    enterprise e
JOIN 
    enterprise_owner eo ON eo.enterprise_id = e.id
JOIN 
    owner o ON o.id = eo.owner_id;
```
