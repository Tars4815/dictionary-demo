# Table: `damage`

**Description (EN):** This table stores the universal, high-level attributes—such as identification and geographical location for all damages following the occurrance of an event. Specific types of damages (like [damages to artistic goods](damage_artistic_good.md), [damages on building functionality](damage_building_functionality.md), or other) store their specialized data in separate sub-tables that share the same ID.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the damage | `3` | PK | No | Acts as the universal ID across all sub-type tables |
| `estimated_value` | BIGINT | [...] | - | - | No | - |
| `component_id` | BIGINT | [...] | - | FK | No | Pointing to id of entity [component](component.md) |
| `date` | TIMESTAMP | [...] | [...] | - | No | - |
| `end_date` | TIMESTAMP | [...] | [...] | - | No | - |
| `start_end` | TIMESTAMP | [...] | [...] | - | No | - |
| `survey_id` | BIGINT | [...] | [...] | FK | No | Pointing to id of entity [survey](survey.md) |
| `country` | VARCHAR | [...] | [...] | - | No | - |
| `county` | VARCHAR | [...] | [...] | - | No | - |
| `description` | VARCHAR | [...] | [...] | - | No | - |
| `hamlet` | VARCHAR | [...] | [...] | - | No | - |
| `house_number` | VARCHAR | [...] | [...] | - | No | - |
| `postcode` | VARCHAR | [...] | [...] | - | No | - |
| `road` | VARCHAR | [...] | [...] | - | No | - |
| `state` | VARCHAR | [...] | [...] | - | No | - |
| `town` | VARCHAR | [...] | [...] | - | No | - |
| `geometry` | GEOMETRY | Spatial representation of the damage entity | [...] | - | No | - |
| `coordinates_inferred` | BOOLEAN | [...] | [...] | - | No | - |
| `sendai_indicator` | VARCHAR | [...] | [...] | - | No | - |

## Relationships

Because `damage` is one of the core entities of the schema, it has extensive relationships:

* **Has Sub-types (Inheritance):** The following tables inherit from `damage` and share its `id`:
    * [`damage_whole_structure`](damage_whole_structure.md)
    * [`damage_vehicles`](damage_vehicles.md)
    * [`damage_people`](damage_people.md)
[...]