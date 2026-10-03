# Table: `damage_network_service`

**Description (EN):** This table represents structural damages to network service. In the database's inheritance architecture, it acts as a direct sub-type of the [`damage`](damage.md) table. It does not store redundant descriptive columns; instead, it uses a shared primary key to inherit all high-level attributes (such as name, location, management type, and geometry) from its parent `damage` record.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the damage to network service | `42` | PK, FK | No | Primary key that also acts as a Foreign Key referencing `damage.id` |
| `affected_users` | BIGINT | [...] | [...] | - | No | [...]|
| `loss_of_service` | BIGINT | [...] | [...] | - | No | [...]|
| `electrical_outage` | VARCHAR | [...] | [...] | - | No | [...]|
| `telecom_outage` | VARCHAR | [...] | [...] | - | No | [...]|
| `transport_outage` | VARCHAR | [...] | [...] | - | No | [...]|

## Relationships
* **Inherits from (Sub-type of):** [`damage`](damage.md). The `damage_network_service` table is a specialized extension of the `damage` table.
* **Affects:** [`component`](component.md) (One or more damages affect a component or its subclasses)
* **Is reported by:** [`survey`](survey.md) (One or more damages is reported in a survey)
* **Reported in:** [`attachment`](attachment.md) (A damage is reported in one or more attachments)
* **Results in:** [`economic_loss`](economic_loss.md)

!!! tip "Where is the rest of the data?"
    To find the name, geographical location (`geometry`, `town`, `country`), or other details of a damage to network service, you must join this table with the `damage` record that shares the exact same `id`.

## Example Query

Retrieve a list of all damages to network service, including their descriptions, towns, and spatial coordinates, by joining the table with its parent `damage` entity:

```sql
SELECT
    dns.*,
    d.*
FROM 
    damage_network_service dns join damage d on dns.id = d.id
```