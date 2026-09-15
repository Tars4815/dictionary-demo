# Table: `survey`

**Description (EN):** This table stores the information and details related to a specific damage assessement survey conducted following a major event.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the survey | `3` | PK | No |[...] |
| `created_on` | TIMESTAMP | Time of execution of the assessment survey | [...] | NOT NULL | No | [...] |
| `enterprise_id` | BIGINT | Time of execution of the assessment survey | [...] | FK | No | Pointing to id of entity [enterprise](enterprise.md) |
| `event_id` | BIGINT | Time of execution of the assessment survey | [...] | FK | No | Pointing to id of entity [event](event.md) |
