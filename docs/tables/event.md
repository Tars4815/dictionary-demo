# Table: `event`

**Description (EN):** This table stores the information and details related to a specific major event.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the event | `3` | PK | No | [...] |
| `date` | TIMESTAMP | Time of occurrence of the event | [...] | - | No | [...] |
| `date_end` | TIMESTAMP | Ending time of occurrence of the event | [...] | - | No | [...] |
| `parent_event_id` | BIGINT | Reference in case of multi-event | [...] | FK | No | Pointing to id of entity [event](event.md) |
| `name` | VARCHAR | [...] | [...] | - | No | - |
| `severity` | VARCHAR | [...] | [...] | - | No | - |
| `type` | VARCHAR | [...] | [...] | - | No | - |
| `country` | VARCHAR | [...] | [...] | - | No | - |
| `state` | VARCHAR | [...] | [...] | - | No | - |
| `county` | VARCHAR | [...] | [...] | - | No | - |
| `town` | VARCHAR | [...] | [...] | - | No | - |
| `hamlet` | VARCHAR | [...] | [...] | - | No | - |
| `road` | VARCHAR | [...] | [...] | - | No | - |
| `house_number` | VARCHAR | [...] | [...] | - | No | - |
| `postcode` | VARCHAR | [...] | [...] | - | No | - |
| `geometry` | GEOMETRY | Spatial representation of the event | [...] | - | Yes | - |
| `coordinates_inferred` | BOOLEAN | [...] | [...] | - | No | - |

## Relationships

* **Has many:** [`survey`](survey.md) (An event can be followed by multiple damage assessment surveys)
* **Is part of / has parts:** [`event`](event.md) through `parent_event_id`. A multi-event can be split into child events that point to the parent event.
