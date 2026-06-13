# Table: `building`

**Description:** This table stores the structural, economic, and physical characteristics of buildings, including construction details, material types, and spatial dimensions. Categorical attributes are managed via CHECK constraints directly within the table definition. It inherits characteristics of the more generic entity [_Enterprise_](enterprise.md).

## Column structure

| Column              | Data type    | Definition                                         | Example value      | Constraint? | Geometry? | Comments                                                                                    |
| :------------------ | :----------- | :------------------------------------------------- | :----------------- | :---------- | :-------- | :------------------------------------------------------------------------------------------ |
| `id`                | BIGINT       | Building unique identifier                         | `3`                | PK, FK      | No        | Primay key that acts as external one for enterprise.id                                      |
| `build_position`    | VARCHAR(255) | Building position                                  | `SINGLE_DETACHED`  | CHECK       | No        | Possible values: SINGLE_DETACHED, SEMI_DETACHED, ROW, NOT_IDENTIFICABLE                     |
| `conservation`      | VARCHAR(255) | Conservation status of the building                | `POORLY_MANTAINED` | CHECK       | No        | Possible values: POORLY_MANTAINED, MODERATELY_MAINTAINED, WELL_MAINTAINED, NOT_IDENTIFIABLE |
| `construction_cost` | INTEGER      | Construction cost                                  | `500000`           |             | No        |                                                                                             |
| `economic_value`    | INTEGER      | Economic value                                     | `1000000`          |             | No        |                                                                                             |
| `floor_area`        | INTEGER      | Metric surface of the floor area                   | `1000`             |             | No        |                                                                                             |
| `floor_height`      | INTEGER      | Average height of floors                           | `4`                |             | No        |                                                                                             |
| `ground_floor`      | VARCHAR(255) | Typology of ground floor                           | `OPEN`             | CHECK       | No        | Possible values: OPEN, CLOSE, NOT_IDENTIFIABLE                                              |
| `horizontal_mat`    | VARCHAR(255) | Construction material of the horizontal structures | `MASONRY_ADOBE`    | CHECK       | No        | Possible values: STEEL, WOORD, MASONRY_ADOBE etc                                            |
| `inhabitants`       | INTEGER      | Number of inhabitants of the given building        | `6`                |             | No        |                                                                                             |
| `n_floors`          | INTEGER      | Number of floors above the ground                  | `3`                |             | No        |                                                                                             |
| `n_under_floors`    | INTEGER      | Number of underground floors                       | `1`                |             | No        |                                                                                             |
| `quality`           | VARCHAR(255) | Overall quality                                    | `GOOD`             |             | No        | Possible values: POOR, GOOD, ACCEPTABLE, NOT_IDENTIFIABLE                                   |
| `regularity`        | VARCHAR(255) | Regularity of structure                            | `NOT_IDENTIFIABLE` | CHECK       | No        | Possible values: NOT_REGULAR, COMPLETELY_REGULAR, etc                                       |
| `retrofitting`      | VARCHAR(255) | Status of retrofitting                             | `NOT_IDENTIFIABLE` | CHECK       | No        | Possible values: NONE, VERTICAL, HORIZONTAL, COMPLETE, NOT_IDENTIFIABLE, etc                |
| `roof_mat`          | VARCHAR(255) | Material of the roof element                       | `NOT_IDENTIFIABLE` | CHECK       | No        | Possible values: STEEL, WOOD, MASONRY_ADOBE, etc                                            |
| `vertical_mat`      | VARCHAR(255) | Material of the vertical structures                | `NOT_IDENTIFIABLE` | CHECK       | No        | Possible values: STEEL, WOOD, MASONRY_ADOBE, etc                                            |
| `year`              | INTEGER      | Construction year                                  | `1999`             |             | No        |                                                                                             |

## Relationships

- **Inherits from (Sub-type of):** [`enterprise`](enterprise.md). The `building` table is an extension of the `enterprise` table.
- **Note:** To find the name, geographical location (`geometry`, `town`, `country`), or VAT of a building, you must look at the `enterprise` record with the exact same `id`.

## Example Query

Retrieve the full details of a building by joining its specific structural data with its general enterprise data (such as name and town):

````sql
SELECT
    e.name,
    e.town,
    b.n_floors,
    b.construction_cost,
    b.economic_value
FROM
    building b
JOIN
    enterprise e ON b.id = e.id
WHERE
    e.type = 'BUILDING';
````
