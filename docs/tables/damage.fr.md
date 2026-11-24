# Table : `damage`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table stocke les attributs universels de haut niveau, comme l'identification et la localisation géographique, de tous les dommages survenus à la suite d'un événement. Les types spécifiques de dommages (comme les [dommages aux biens artistiques](damage_artistic_good.md), les [dommages à la fonctionnalité des bâtiments](damage_building_functionality.md) ou d'autres) stockent leurs données spécialisées dans des sous-tables distinctes qui partagent le même identifiant.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique du dommage | `3` | PK | Non | Sert d'identifiant universel pour toutes les tables de sous-types |
| `estimated_value` | BIGINT | [...] | - | - | Non | - |
| `component_id` | BIGINT | [...] | - | FK | Non | Pointe vers l'id de l'entité [component](component.md) |
| `date` | TIMESTAMP | [...] | [...] | - | Non | - |
| `end_date` | TIMESTAMP | [...] | [...] | - | Non | - |
| `start_end` | TIMESTAMP | [...] | [...] | - | Non | - |
| `survey_id` | BIGINT | [...] | [...] | FK | Non | Pointe vers l'id de l'entité [survey](survey.md) |
| `country` | VARCHAR | [...] | [...] | - | Non | - |
| `county` | VARCHAR | [...] | [...] | - | Non | - |
| `description` | VARCHAR | [...] | [...] | - | Non | - |
| `hamlet` | VARCHAR | [...] | [...] | - | Non | - |
| `house_number` | VARCHAR | [...] | [...] | - | Non | - |
| `postcode` | VARCHAR | [...] | [...] | - | Non | - |
| `road` | VARCHAR | [...] | [...] | - | Non | - |
| `state` | VARCHAR | [...] | [...] | - | Non | - |
| `town` | VARCHAR | [...] | [...] | - | Non | - |
| `geometry` | GEOMETRY | Représentation spatiale de l'entité dommage | [...] | - | Non | - |
| `coordinates_inferred` | BOOLEAN | [...] | [...] | - | Non | - |
| `sendai_indicator` | VARCHAR | [...] | [...] | - | Non | - |

## Relations

Comme `damage` est l'une des entités centrales du schéma, elle a de nombreuses relations :

* **A des sous-types (héritage) :** Les tables suivantes héritent de `damage` et partagent son `id` :
    * [`damage_artistic_good`](damage_artistic_good.md)
    * [`damage_building_functionality`](damage_building_functionality.md)
    * [`damage_building_not_structural`](damage_building_not_structural.md)
    * [`damage_building_structural`](damage_building_structural.md)
    * [`damage_business_operations`](damage_business_operations.md)
    * [`damage_church_structure`](damage_church_structure.md)
    * [`damage_goods`](damage_goods.md)
    * [`damage_network_component`](damage_network_component.md)
    * [`damage_network_service`](damage_network_service.md)
    * [`damage_people`](damage_people.md)
    * [`damage_product`](damage_product.md)
    * [`damage_vehicles`](damage_vehicles.md)
    * [`damage_whole_structure`](damage_whole_structure.md)
    * [`farm_damage`](farm_damage.md)
* **Affecte :** [`component`](component.md) (Un ou plusieurs dommages affectent un composant ou ses sous-classes)
* **Est enregistré par :** [`survey`](survey.md) (Un ou plusieurs dommages sont signalés dans un relevé)
* **Est documenté dans :** [`attachment`](attachment.md) (Un dommage est signalé dans une ou plusieurs pièces jointes)
* **Entraîne :** [`economic_loss`](economic_loss.md)