# Table: `survey`

**Description (EN):** This table stores the information and details related to a specific damage assessement survey conducted following a major event.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the survey | `3` | PK | No |[...] |
| `created_on` | TIMESTAMP | Time of execution of the assessment survey | [...] | NOT NULL | No | [...] |
| `enterprise_id` | BIGINT | Foreign key referring to an enterprise | [...] | FK | No | Pointing to id of entity [enterprise](enterprise.md) |
| `event_id` | BIGINT | Time of execution of the assessment survey | [...] | FK | No | Pointing to id of entity [event](event.md) |

## Relationships

Because `survey` is one of the core entities of the schema, it has extensive relationships:

* **Reports** [`damage`](damage.md)
* **Is linked to** [`enterprise`](enterprise.md)
* **Follows an** [`event`](event.md)