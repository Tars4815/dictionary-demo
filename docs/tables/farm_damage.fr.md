# Table : `farm_damage`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table représente les dommages signalés aux exploitations agricoles. Dans l'architecture d'héritage de la base de données, elle joue le rôle de sous-type direct de la table [`damage`](damage.md). Elle ne stocke pas de colonnes descriptives redondantes : elle utilise à la place une clé primaire partagée pour hériter de tous les attributs de haut niveau (comme la description, les dates, la localisation et la géométrie) de son enregistrement parent `damage`.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique du dommage à une exploitation agricole | `42` | PK, FK | Non | Clé primaire qui joue aussi le rôle de clé étrangère référençant `damage.id` |

## Relations

* **Hérite de (sous-type de) :** [`damage`](damage.md). La table `farm_damage` est une extension spécialisée de la table `damage`.
* **Affecte :** [`component`](component.md) (Un ou plusieurs dommages affectent un composant ou ses sous-classes)
* **Est signalé par :** [`survey`](survey.md) (Un ou plusieurs dommages sont signalés dans un relevé)
* **Signalé dans :** [`attachment`](attachment.md) (Un dommage est signalé dans une ou plusieurs pièces jointes)
* **Entraîne :** [`economic_loss`](economic_loss.md)
* **A des sous-types (héritage) :** Les tables suivantes héritent de `farm_damage` et partagent son `id` :
    * [`damage_agriculture_product`](damage_agriculture_product.md)
    * [`damage_fixed_asset`](damage_fixed_asset.md)
    * [`damage_livestock`](damage_livestock.md)
    * [`damage_provision`](damage_provision.md)
    * [`damage_staff`](damage_staff.md)

!!! tip "Où trouver le reste des données ?"
    Pour trouver la description, les dates, la localisation géographique (`geometry`, `town`, `country`) ou d'autres informations sur un dommage aux exploitations agricoles, vous devez joindre cette table à l'enregistrement `damage` qui partage le même `id`.

## Exemple de requête

Récupérez la liste de tous les dommages aux exploitations agricoles, avec leurs descriptions, communes et coordonnées spatiales, en joignant la table à son entité parente `damage` :

```sql
SELECT
    fd.*,
    d.*
FROM 
    farm_damage fd JOIN damage d ON fd.id = d.id;
```
