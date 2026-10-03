# Table: `event`

**Description (EN):** This table stores the information and details related to a specific major event.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the event | `3` | PK | No | [...] |
| `date` | TIMESTAMP | Time of occurrence of the event | [...] | - | No | [...] |
| `date_end` | TIMESTAMP | Ending time of occurrence of the event | [...] | - | No | [...] |
| `parent_event_id` | BIGINT | Reference in case of multi-event | [...] | FK | No | Pointing to id of entity [event](event.md) |
| `name` | VARCHAR | Name of the event | `Storm Example` | - | No | - |
| `severity` | VARCHAR | Severity level of the event | [...] | - | No | - |
| `type` | VARCHAR | Type of the event | [...] | - | No | - |
| `country` | VARCHAR | Country where the event is located | `Italy` | - | No | - |
| `state` | VARCHAR | State or region where the event is located | `Lazio` | - | No | - |
| `county` | VARCHAR | County or province where the event is located | `Rome` | - | No | - |
| `town` | VARCHAR | Municipality where the event is located | `Rome` | - | No | - |
| `hamlet` | VARCHAR | Hamlet or locality where the event is located | `Trastevere` | - | No | - |
| `road` | VARCHAR | Street where the event is located | `Via Appia` | - | No | - |
| `house_number` | VARCHAR | House number of the event | `10` | - | No | - |
| `postcode` | VARCHAR | Postal code of the event | `00100` | - | No | - |
| `geometry` | GEOMETRY | Spatial representation of the event | [...] | - | Yes | - |
| `coordinates_inferred` | BOOLEAN | Whether the coordinates of the event were inferred rather than directly measured | [...] | - | No | - |

## Relationships

* **Has many:** [`survey`](survey.md) (An event can be followed by multiple damage assessment surveys)
* **Is part of / has parts:** [`event`](event.md) through `parent_event_id`. A multi-event can be split into child events that point to the parent event.
