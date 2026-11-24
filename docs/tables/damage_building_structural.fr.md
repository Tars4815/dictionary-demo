# Table : `damage_building_structural`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table représente les dommages structurels aux fonctionnalités des bâtiments. Dans l'architecture d'héritage de la base de données, elle joue le rôle de sous-type direct de la table [`damage`](damage.md). Elle ne stocke pas de colonnes descriptives redondantes : elle utilise à la place une clé primaire partagée pour hériter de tous les attributs de haut niveau (comme le nom, la localisation, le type de gestion et la géométrie) de son enregistrement parent `damage`.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique du dommage structurel à un bâtiment | `42` | PK, FK | Non | Clé primaire qui joue aussi le rôle de clé étrangère référençant `damage.id` |
| `extension` | BIGINT | [...] | [...] | - | Non | [...] |
| `level` | VARCHAR | [...] | [...] | - | Non | [...] |
| `classification` | VARCHAR | [...] | [...] | - | Non | [...] |

## Relations

* **Hérite de (sous-type de) :** [`damage`](damage.md). La table `damage_building_structural` est une extension spécialisée de la table `damage`.
* **Affecte :** [`component`](component.md) (Un ou plusieurs dommages affectent un composant ou ses sous-classes)
* **Est signalé par :** [`survey`](survey.md) (Un ou plusieurs dommages sont signalés dans un relevé)
* **Signalé dans :** [`attachment`](attachment.md) (Un dommage est signalé dans une ou plusieurs pièces jointes)
* **Entraîne :** [`economic_loss`](economic_loss.md)

!!! tip "Où trouver le reste des données ?"
    Pour trouver le nom, la localisation géographique (`geometry`, `town`, `country`) ou d'autres informations sur un dommage structurel aux bâtiments, vous devez joindre cette table à l'enregistrement `damage` qui partage le même `id`.

## Exemple de requête

Récupérez la liste de tous les dommages structurels aux bâtiments, avec leurs noms, communes et coordonnées spatiales, en joignant la table à son entité parente `damage` :

```sql
SELECT
    dbs.*,
    d.*
FROM 
    damage_building_structural dbs  join damage d on dbs.id = d.id
```