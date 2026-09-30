# Table: `enterprise_owner`

**Description (EN):** This entity acts as the linking table for the many-to-many relationship between [`enterprise`](enterprise.md) and [`owner`](owner.md).

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `enterprise_id` | BIGINT | Identifier for the enterprise| `3` | FK | No | References the `enterprise` table |
| `owner_id` | BIGINT | Identifier for the owner| `8` | FK | No | References the `owner` table |


