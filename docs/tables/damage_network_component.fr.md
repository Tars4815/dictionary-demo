# Table : `damage_network_component`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table représente les dommages structurels aux composants de réseau. Dans l'architecture d'héritage de la base de données, elle joue le rôle de sous-type direct de la table [`damage`](damage.md). Elle ne stocke pas de colonnes descriptives redondantes : elle utilise à la place une clé primaire partagée pour hériter de tous les attributs de haut niveau (comme le nom, la localisation, le type de gestion et la géométrie) de son enregistrement parent `damage`.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique du dommage aux composants de réseau | `42` | PK, FK | Non | Clé primaire qui joue aussi le rôle de clé étrangère référençant `damage.id` |
| `reachable` | BOOLEAN | [...] | [...] | - | Non | [...] |
| `network_damage_level` | VARCHAR | [...] | [...] | - | Non | [...] |
| `electrical_damage_category` | VARCHAR | [...] | [...] | - | Non | [...] |
| `transport_damage_category` | VARCHAR | [...] | [...] | - | Non | [...] |

## Relations

* **Hérite de (sous-type de) :** [`damage`](damage.md). La table `damage_network_component` est une extension spécialisée de la table `damage`.
* **Affecte :** [`component`](component.md) (Un ou plusieurs dommages affectent un composant ou ses sous-classes)
* **Est signalé par :** [`survey`](survey.md) (Un ou plusieurs dommages sont signalés dans un relevé)
* **Signalé dans :** [`attachment`](attachment.md) (Un dommage est signalé dans une ou plusieurs pièces jointes)
* **Entraîne :** [`economic_loss`](economic_loss.md)

!!! tip "Où trouver le reste des données ?"
    Pour trouver le nom, la localisation géographique (`geometry`, `town`, `country`) ou d'autres informations sur un dommage aux composants de réseau, vous devez joindre cette table à l'enregistrement `damage` qui partage le même `id`.

## Exemple de requête

Récupérez la liste de tous les dommages aux composants de réseau, avec leurs descriptions, communes et coordonnées spatiales, en joignant la table à son entité parente `damage` :

```sql
SELECT
    dnc.*,
    d.*
FROM 
    damage_network_component dnc   join damage d on dnc.id = d.id
```