# Table : `farm`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table représente les entreprises agricoles. Dans l'architecture d'héritage de la base de données, elle joue le rôle de sous-type direct de la table [`enterprise`](enterprise.md). Elle ne stocke pas de colonnes descriptives redondantes : elle utilise à la place une clé primaire partagée pour hériter de tous les attributs de haut niveau (comme le nom, la localisation, le type de gestion et la géométrie) de son enregistrement parent `enterprise`.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique de l'exploitation agricole | `42` | PK, FK | Non | Clé primaire qui joue aussi le rôle de clé étrangère référençant `enterprise.id` |

## Relations

* **Hérite de (sous-type de) :** [`enterprise`](enterprise.md). La table `farm` est une extension spécialisée de la table `enterprise`.
* **Contient :** Bien qu'elle ne soit pas liée directement via `farm_id`, une exploitation agricole possède des actifs agricoles par la colonne `enterprise_id` de la table `component`. Ces composants incluent souvent des sous-types agricoles spécialisés, tels que :
    * [`agriculture_product`](agriculture_product.md) et ses sous-types [`crop`](crop.md) et [`stored`](stored.md)
    * [`livestock`](livestock.md)
    * [`fixed_asset`](fixed_asset.md) et ses sous-types (p. ex. [`machinery`](machinery.md), comme les tracteurs)

!!! tip "Où trouver le reste des données ?"
    Pour trouver le nom, la localisation géographique (`geometry`, `town`, `country`) ou d'autres informations sur une exploitation agricole, vous devez joindre cette table à l'enregistrement `enterprise` qui partage le même `id`.

## Exemple de requête

Récupérez la liste de toutes les exploitations agricoles, avec leurs noms, communes et coordonnées spatiales, en joignant la table à son entité parente `enterprise` :

```sql
SELECT 
    f.id, 
    e.name, 
    e.town, 
    ST_AsText(e.geometry) as coordinates 
FROM 
    farm f
JOIN 
    enterprise e ON f.id = e.id
WHERE 
    e.type = 'FARM';
```
