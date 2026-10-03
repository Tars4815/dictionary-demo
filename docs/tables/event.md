# Table: `event`

**Description (EN):** This table stores the information and details related to a specific a major event.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the survey | `3` | PK | No |[...] |
| `date` | TIMESTAMP | Time of occurrance of the event | [...] | NOT NULL | No | [...] |
| `date_end` | TIMESTAMP | Ending time of occurrance of the event | [...] | NOT NULL | No | [...] |
| `parent_event_id` | BIGINT | Reference in case of multi-event | [...] | FK | No | Pointing to id of entity [event](event.md) |
| `name` | VARCHAR | [...] | [...] | - | No | - |
| `severity` | VARCHAR | [...] | [...] | - | No | - |
| `type` | VARCHAR | [...] | [...] | - | No | - |
| `country` | VARCHAR | [...] | [...] | - | No | - |
| `county` | VARCHAR | [...] | [...] | - | No | - |
| `hamlet` | VARCHAR | [...] | [...] | - | No | - |
| `state` | VARCHAR | [...] | [...] | - | No | - |
| `town` | VARCHAR | [...] | [...] | - | No | - |
| `coordinates_inferred` | BOOLEAN | [...] | [...] | - | No | - |

## Relationships

Because `event` is one of the core entities of the schema, it has extensive relationships:

* **Is followed by** [`survey`](survey.md)
* **Is combined with** [`event`](event.md). In case of multi-event scenario, a record of this entity can be linked to another event.