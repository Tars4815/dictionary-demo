# Table: `enterprise`

**Description (EN):** This is the core parent entity (superclass) of the database. It stores the universal, high-level attributes—such as identification, geographical location, and ownership details—for all major physical or business assets. Specific types of enterprises (like [buildings](building.md), [farms](farm.md), or network systems) store their specialized data in separate sub-tables that share the same ID.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the enterprise | `3` | PK | No | Acts as the universal ID across all sub-type tables |
| `type` | VARCHAR(255) | Discriminator column defining the specific type of enterprise | `BUILDING` | NOT NULL | No | Expected values: 'BUILDING', 'FARM', 'NETWORK_SYSTEM' |
| `name` | VARCHAR(255) | Official name or denomination of the enterprise | `Main Headquarters` | | No | |
| `management_type` | VARCHAR(255) | Type of management or business administration | `PUBLIC` | | No | e.g., 'PUBLIC', 'PRIVATE', 'MIXED' |
| `town` | VARCHAR(255) | Municipality where the enterprise is located | `Rome` | | No | |
| `country` | VARCHAR(255) | Country where the enterprise is located | `Italy` | | No | |
| `geometry` | GEOMETRY | Spatial representation of the enterprise | `POINT(12.49 41.89)` | | Yes | EPSG:4326. Can be a Point or a Polygon depending on the scale |
| `owner_id` | BIGINT | Identifier of the entity's owner | `42` | FK | No | References the `owner` table |

## Relationships

Because `enterprise` is the central hub of the schema, it has extensive relationships:

* **Has Sub-types (Inheritance):** The following tables inherit from `enterprise` and share its `id`:
    * [`building`](building.md)
    * [`farm`](farm.md)
    * [`network_system`](network_system.md)
* **Belongs to:** `owner` (An enterprise is owned by an owner)
* **Has many:** [`component`](component.md) (An enterprise is composed of multiple sub-components like machinery, crops, or electrical networks)
* **Has many:** `survey` (An enterprise can undergo multiple damage or assessment surveys over time)

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