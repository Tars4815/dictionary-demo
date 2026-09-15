# Table: `event`

**Description (EN):** This table stores the information and details related to a specific a major event.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the survey | `3` | PK | No |[...] |
| `date` | TIMESTAMP | Time of occurrance of the event | [...] | NOT NULL | No | [...] |
| `date_end` | TIMESTAMP | Ending time of occurrance of the event | [...] | NOT NULL | No | [...] |
| `parente_event_id` | BIGINT | Reference in case of multi-event | [...] | FK | No | Pointing to id of entity [event](event.md) |
| `name` | VARCHAR | [...] | [...] | - | No | - |
| `severity` | VARCHAR | [...] | [...] | - | No | - |
| `type` | VARCHAR | [...] | [...] | - | No | - |
| `country` | VARCHAR | [...] | [...] | - | No | - |
| `county` | VARCHAR | [...] | [...] | - | No | - |
| `hamlet` | VARCHAR | [...] | [...] | - | No | - |
| `state` | VARCHAR | [...] | [...] | - | No | - |
| `town` | VARCHAR | [...] | [...] | - | No | - |