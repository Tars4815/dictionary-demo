# Table : `component`

!!! info "Nom différent dans l'interface web (GUI)"
    Dans le backend PostgreSQL, cette table s'appelle `component`, comme indiqué dans le titre de la page. Dans l'interface de l'application web, elle apparaît sous le nom **Elements & production (all subclasses)**. Tous les alias figurent dans le [tableau de correspondance](../backend-to-gui.md).

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table stocke les attributs universels de haut niveau, comme l'identification et la localisation géographique, de tous les principaux composants physiques ou commerciaux. Les types spécifiques de composants (comme les [blocs ajoutés](added_block.md), les [biens artistiques](artistic_good.md) ou d'autres) stockent leurs données spécialisées dans des sous-tables distinctes qui partagent le même identifiant.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique du composant | `3` | PK | Non | Sert d'identifiant universel pour toutes les tables de sous-types |
| `component_kind` | VARCHAR | Colonne discriminante identifiant le sous-type spécifique du composant | `BUILDING_COMPONENT` | NOT NULL | Non | Contient le type le plus spécifique. Valeurs actuellement présentes dans les données : 'BUILDING_COMPONENT', 'TRANSPORT_COMPONENT', 'TRANSPORT_SERVICE', 'ADDED_BLOCK', 'CROP' |
| `enterprise_id` | BIGINT | Identifiant de l'entreprise à laquelle appartient le composant | `42` | FK | Non | Pointe vers l'id de l'entité [enterprise](enterprise.md) |
| `insured` | BOOLEAN | Indique si le composant est couvert par une assurance | `True` | - | Non | - |
| `name` | VARCHAR | Nom ou dénomination du composant | `Warehouse A` | - | Non | - |
| `country` | VARCHAR | Pays où se trouve le composant | `Italy` | - | Non | - |
| `state` | VARCHAR | État ou région où se trouve le composant | `Lazio` | - | Non | - |
| `county` | VARCHAR | Comté ou province où se trouve le composant | `Rome` | - | Non | - |
| `town` | VARCHAR | Commune où se trouve le composant | `Rome` | - | Non | - |
| `hamlet` | VARCHAR | Hameau ou lieu-dit où se trouve le composant | `Trastevere` | - | Non | - |
| `road` | VARCHAR | Rue où se trouve le composant | `Via Appia` | - | Non | - |
| `house_number` | VARCHAR | Numéro de voie du composant | `10` | - | Non | - |
| `postcode` | VARCHAR | Code postal du composant | `00100` | - | Non | - |
| `details` | VARCHAR | Précisions complémentaires sur l'adresse du composant | `Building B, second floor` | - | Non | - |
| `geometry` | GEOMETRY | Représentation spatiale de l'entité composant | [...] | - | Oui | - |
| `coordinates_inferred` | BOOLEAN | Indique si les coordonnées du composant ont été déduites plutôt que mesurées directement | [...] | - | Non | - |
| `cultural_heritage` | BOOLEAN | Indique si le composant est un élément du patrimoine culturel | [...] | - | Non | - |

## Relations

Comme `component` est l'une des entités centrales du schéma, elle a de nombreuses relations :

* **A des sous-types (héritage) :** Les tables suivantes héritent de `component` et partagent son `id` :
    * [`added_block`](added_block.md)
    * [`artistic_good`](artistic_good.md)
    * [`agriculture_product`](agriculture_product.md), qui a ses propres sous-types [`crop`](crop.md) et [`stored`](stored.md)
    * [`building_component`](building_component.md)
    * [`building_functionality`](building_functionality.md)
    * [`business_operations`](business_operations.md)
    * [`electrical_network_component`](electrical_network_component.md)
    * [`fixed_asset`](fixed_asset.md), qui a ses propres sous-types [`infrastructure`](infrastructure.md), [`land`](land.md), [`machinery`](machinery.md) et [`material`](material.md)
    * [`livestock`](livestock.md)
    * [`network_service`](network_service.md)
    * [`product`](product.md)
    * [`provision`](provision.md)
    * [`staff`](staff.md)
    * [`tlc_network_component`](tlc_network_component.md)
    * [`transport_network_component`](transport_network_component.md)
* **Appartient à :** [`enterprise`](enterprise.md) (Un composant est lié à une seule entreprise)
* **A plusieurs :** [`damage`](damage.md) (Un composant peut subir plusieurs dommages au fil du temps)
