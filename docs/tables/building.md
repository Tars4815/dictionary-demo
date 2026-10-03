# Table: `building`

**Description:** This table stores the structural, economic, and physical characteristics of buildings, including construction details, material types, and spatial dimensions. Categorical attributes are managed via CHECK constraints directly within the table definition. It inherits characteristics of the more generic entity [_Enterprise_](enterprise.md).

## Column structure

| Column              | Data type    | Definition                                         | Example value      | Constraint? | Geometry? | Comments                                                                                    |
| :--------- | :----------- | :-------------- | :----------------- | :---------- | :-------- | :------------------------------------------------------------------------------------------ |
| `id`                | BIGINT       | Building unique identifier                         | `3`                | PK, FK      | No        | Primay key that acts as external one for enterprise.id                    |              

## Relationships

- **Inherits from (Sub-type of):** [`enterprise`](enterprise.md). The `building` table is an extension of the `enterprise` table.
- **Note:** To find the name, geographical location (`geometry`, `town`, `country`), or VAT of a building, you must look at the `enterprise` record with the exact same `id`.

## Example Query

Retrieve the full details of a building by joining its specific structural data with its general enterprise data (such as name and town):

````sql
SELECT
    e.name,
    e.town,
    b.*
FROM
    building b
JOIN
    enterprise e ON b.id = e.id
WHERE
    e.type = 'BUILDING';
````
