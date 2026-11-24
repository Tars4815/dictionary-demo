# Table : `damage_fixed_asset`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table représente les dommages signalés aux immobilisations des exploitations agricoles. Dans l'architecture d'héritage de la base de données, elle joue le rôle de sous-type direct de la table [`farm_damage`](farm_damage.md), qui est elle-même un sous-type de [`damage`](damage.md). Elle ne stocke pas de colonnes descriptives redondantes : elle utilise à la place une clé primaire partagée pour hériter de tous les attributs de haut niveau (comme la description, les dates, la localisation et la géométrie) de son enregistrement parent `damage`.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique du dommage à une immobilisation d'une exploitation agricole | `42` | PK, FK | Non | Clé primaire qui joue aussi le rôle de clé étrangère référençant `farm_damage.id` (et, à son tour, `damage.id`) |
| `perc_area` | DOUBLE PRECISION | Pourcentage de la superficie touchée | [...] | - | Non | - |
| `size` | DOUBLE PRECISION | Taille de l'immobilisation touchée | [...] | - | Non | - |

## Relations

* **Hérite de (sous-type de) :** [`farm_damage`](farm_damage.md), qui hérite à son tour de [`damage`](damage.md). La table `damage_fixed_asset` est une extension spécialisée de la table `farm_damage`.
* **Affecte :** [`component`](component.md) (Un ou plusieurs dommages affectent un composant ou ses sous-classes)
* **Est signalé par :** [`survey`](survey.md) (Un ou plusieurs dommages sont signalés dans un relevé)
* **Signalé dans :** [`attachment`](attachment.md) (Un dommage est signalé dans une ou plusieurs pièces jointes)
* **Entraîne :** [`economic_loss`](economic_loss.md)

!!! tip "Où trouver le reste des données ?"
    Pour trouver la description, les dates, la localisation géographique (`geometry`, `town`, `country`) ou d'autres informations sur un dommage aux immobilisations des exploitations agricoles, vous devez joindre cette table à l'enregistrement `damage` qui partage le même `id`.

## Exemple de requête

Récupérez la liste de tous les dommages aux immobilisations des exploitations agricoles, avec leurs descriptions, communes et coordonnées spatiales, en joignant la table à son entité parente `damage` :

```sql
SELECT
    dfa.*,
    d.*
FROM 
    damage_fixed_asset dfa JOIN damage d ON dfa.id = d.id;
```
