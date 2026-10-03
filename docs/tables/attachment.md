# Table: `attachment`

**Description (EN):** This table stores the information and details related to an attachment.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the attachment | `3` | PK | No |[...] |
| `damage_id` | BIGINT | Foreign key referring to a reported damage | [...] | FK | No | Pointing to id of entity [damage](damage.md) |
| `date` | TIMESTAMP | [...] | - | - | No | - |
| `size` | BIGINT | [...] | - | - | No | - |
| `description` | VARCHAR | [...] | - | - | No | - |
| `name` | VARCHAR | [...] | - | - | No | - |
| `type` | VARCHAR | [...] | - | - | No | - |
| `data` | BIGINT | [...] | - | - | No | - |

## Relationships

* **Documents** [`damage`](damage.md)