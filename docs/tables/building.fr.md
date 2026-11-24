# Table : `building`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table représente les bâtiments. Dans l'architecture d'héritage de la base de données, elle joue le rôle de sous-type direct de la table [`enterprise`](enterprise.md). Elle ne stocke pas de colonnes descriptives redondantes : elle utilise à la place une clé primaire partagée pour hériter de tous les attributs de haut niveau (comme le nom, la localisation, le type de gestion et la géométrie) de son enregistrement parent `enterprise`.

Les caractéristiques structurelles, économiques et physiques d'un bâtiment (année de construction, matériaux, nombre d'étages, coût, etc.) sont stockées dans la table [`building_component`](building_component.md).

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique du bâtiment | `3` | PK, FK | Non | Clé primaire qui joue aussi le rôle de clé étrangère référençant `enterprise.id` |

## Relations

* **Hérite de (sous-type de) :** [`enterprise`](enterprise.md). La table `building` est une extension spécialisée de la table `enterprise`.
* **Contient :** Bien qu'il ne soit pas lié directement via `building_id`, un bâtiment possède ses parties physiques par la colonne `enterprise_id` de la table `component`. Ces composants incluent souvent des sous-types spécialisés, tels que :
    * [`building_component`](building_component.md)
    * [`added_block`](added_block.md)
    * [`building_functionality`](building_functionality.md)

!!! tip "Où trouver le reste des données ?"
    Pour trouver le nom, la localisation géographique (`geometry`, `town`, `country`) ou le numéro de TVA d'un bâtiment, vous devez joindre cette table à l'enregistrement `enterprise` qui partage le même `id`. Les caractéristiques structurelles et économiques se trouvent dans `building_component`, qui est liée au bâtiment par `component.enterprise_id`.

## Exemple de requête

Récupérez les caractéristiques de chaque bâtiment en joignant son enregistrement d'entreprise à ses composants de bâtiment :

```sql
SELECT
    e.name,
    e.town,
    bc.n_floors,
    bc.construction_cost,
    bc.economic_value
FROM
    building b
JOIN
    enterprise e ON b.id = e.id
JOIN
    component c ON c.enterprise_id = e.id
JOIN
    building_component bc ON bc.id = c.id
WHERE
    e.type = 'BUILDING';
```
