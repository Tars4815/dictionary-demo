# Table: `economic_loss`

**Description (EN):** This table stores the information and details related to a specific damage assessement survey conducted following a major event.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the survey | `3` | PK | No |[...] |
| `damage_id` | BIGINT | Foreign key referring to a reported damage | [...] | FK | No | Pointing to id of entity [damage](damage.md) |
| `approved_cost` | BIGINT | [...] | - | - | No | - |
| `estimated_cost` | BIGINT | [...] | - | - | No | - |
| `final_cost` | BIGINT | [...] | - | - | No | - |
| `type_of_cost` | BIGINT | [...] | - | - | No | - |

## Relationships

* **Is the result of** [`damage`](damage.md)