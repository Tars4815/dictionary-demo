# Table : `enterprise`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Il s'agit de l'entité parente centrale (superclasse) de la base de données. Elle stocke les attributs universels de haut niveau, comme l'identification, la localisation géographique et les informations administratives, de tous les principaux actifs physiques ou commerciaux. Les types spécifiques d'entreprises (comme les [bâtiments](building.md), les [entreprises commerciales](business.md), les [exploitations agricoles](farm.md) ou les [systèmes de réseau](network_system.md)) stockent leurs données spécialisées dans des sous-tables distinctes qui partagent le même identifiant. La propriété n'est pas stockée ici : elle est enregistrée dans la table de liaison [`enterprise_owner`](enterprise_owner.md).

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique de l'entreprise | `3` | PK | Non | Sert d'identifiant universel pour toutes les tables de sous-types |
| `type` | VARCHAR(255) | Colonne discriminante définissant le type spécifique d'entreprise | `BUILDING` | NOT NULL | Non | Valeurs actuellement présentes dans les données : 'BUILDING', 'FARM', 'TRANSPORT', 'TELECOMMUNICATION' |
| `name` | VARCHAR(255) | Nom officiel ou dénomination de l'entreprise | `Main Headquarters` |  | Non |  |
| `management_type` | VARCHAR(255) | Type de gestion ou d'administration de l'entreprise | `PUBLIC` |  | Non | e.g., 'PUBLIC', 'PRIVATE', 'MIXED' |
| `vat` | VARCHAR(255) | Numéro de TVA de l'entreprise | `IT00000000000` |  | Non |  |
| `description` | VARCHAR(255) | Description en texte libre de l'entreprise | `Regional hospital` |  | Non |  |
| `country` | VARCHAR(255) | Pays où se trouve l'entreprise | `Italy` |  | Non |  |
| `state` | VARCHAR(255) | État ou région où se trouve l'entreprise | `Lazio` |  | Non |  |
| `county` | VARCHAR(255) | Comté ou province où se trouve l'entreprise | `Rome` |  | Non |  |
| `town` | VARCHAR(255) | Commune où se trouve l'entreprise | `Rome` |  | Non |  |
| `hamlet` | VARCHAR(255) | Hameau ou lieu-dit où se trouve l'entreprise | `Trastevere` |  | Non |  |
| `road` | VARCHAR(255) | Rue où se trouve l'entreprise | `Via Appia` |  | Non |  |
| `house_number` | VARCHAR(255) | Numéro de voie de l'entreprise | `10` |  | Non |  |
| `postcode` | VARCHAR(255) | Code postal de l'entreprise | `00100` |  | Non |  |
| `geometry` | GEOMETRY | Représentation spatiale de l'entreprise | `POINT(12.49 41.89)` |  | Oui | EPSG:4326. Peut être un point ou un polygone selon l'échelle |
| `coordinates_inferred` | BOOLEAN | Indique si les coordonnées de l'entreprise ont été déduites plutôt que mesurées directement | [...] |  | Non |  |

## Relations

Comme `enterprise` est le pivot central du schéma, elle a de nombreuses relations :

* **A des sous-types (héritage) :** Les tables suivantes héritent de `enterprise` et partagent son `id` :
    * [`building`](building.md)
    * [`business`](business.md)
    * [`farm`](farm.md)
    * [`network_system`](network_system.md)
* **Est détenue par :** [`owner`](owner.md). Une entreprise peut avoir plusieurs propriétaires, et un propriétaire peut détenir plusieurs entreprises. Cette relation plusieurs-à-plusieurs est assurée par la table de liaison [`enterprise_owner`](enterprise_owner.md).
* **A plusieurs :** [`component`](component.md) (Une entreprise est composée de plusieurs sous-composants, comme des machines, des cultures ou des réseaux électriques)
* **A plusieurs :** [`survey`](survey.md) (Une entreprise peut faire l'objet de plusieurs dommages ou relevés d'évaluation au fil du temps)

## Exemple de requête

Récupérez la liste de toutes les entreprises situées dans une commune donnée, en affichant leur nom, leur classification spécifique (type) et leurs coordonnées :

```sql
SELECT 
    id, 
    name, 
    type, 
    ST_AsText(geometry) as coordinates 
FROM 
    enterprise 
WHERE 
    town = 'Rome'
ORDER BY 
    type ASC;
```

Récupérez les propriétaires de chaque entreprise via la table de liaison :

```sql
SELECT 
    e.id, 
    e.name, 
    o.full_name 
FROM 
    enterprise e
JOIN 
    enterprise_owner eo ON eo.enterprise_id = e.id
JOIN 
    owner o ON o.id = eo.owner_id;
```
