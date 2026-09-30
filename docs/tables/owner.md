# Table: `owner`

**Description (EN):** This entity stores the universal, high-level attributes—such as identification and contacts for owner records.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the owner | `3` | PK | No | - |
| `email` | VARCHAR | Email address of the owner | `example@mail.com` | - | No | - |
| `fiscal_code` | VARCHAR | Fiscal code of the owner | `AB0123CDEF` | - | No | Character limit and configuration can vary from country to country |
| `full_name` | VARCHAR | Full name of the owner | `John Doe` | - | No | - |
| `phone` | VARCHAR | Phone number and international prefix of the owner | `+390123456789` | - | No | - |

## Relationships

* **Owns:** [`enterprise`](enterprise.md) (An owner owns an enterprirse). This many-to-many relationship is mediated with the [`enterprise_owner`](enterprise_owner.md) bridge table.

## Example Query

Retrieve a list of all owner, displaying their name and their specific contacts:

```sql
SELECT *
FROM 
    owner o
ORDER BY 
    o.full_name ASC;
```

