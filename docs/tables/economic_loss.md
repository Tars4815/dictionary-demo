# Table: `economic_loss`

**Description (EN):** This table stores the costs associated with a reported damage: the estimated, approved and final amounts.

## Column Structure

| Column | Data type | Definition | Example value | Constraint? | Geometry? | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Unique identifier for the economic loss record | `3` | PK | No | [...] |
| `damage_id` | BIGINT | Foreign key referring to a reported damage | [...] | FK | No | Pointing to id of entity [damage](damage.md) |
| `approved_cost` | DOUBLE PRECISION | Cost approved for the damage | - | - | No | - |
| `estimated_cost` | DOUBLE PRECISION | Estimated cost of the damage | - | - | No | - |
| `final_cost` | DOUBLE PRECISION | Final cost of the damage | - | - | No | - |
| `type_of_cost` | VARCHAR | Type of cost | - | - | No | - |

## Relationships

* **Refers to:** [`damage`](damage.md) through `damage_id`. The economic loss is the monetary result of a reported damage.

## Example Query

Retrieve the costs recorded for each damage:

```sql
SELECT 
    d.id AS damage_id, 
    el.type_of_cost, 
    el.estimated_cost, 
    el.approved_cost, 
    el.final_cost 
FROM 
    economic_loss el
JOIN 
    damage d ON el.damage_id = d.id;
```
