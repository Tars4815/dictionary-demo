# Table : `tlc_system`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table représente les systèmes de réseau de télécommunications. Dans l'architecture d'héritage de la base de données, elle joue le rôle de sous-type direct de la table [`network_system`](network_system.md). Elle ne stocke pas de colonnes descriptives redondantes : elle utilise à la place une clé primaire partagée pour hériter de tous les attributs de haut niveau (comme le nom, la localisation, le type de gestion et la géométrie) de son enregistrement parent `network_system`, lui-même enfant d'un enregistrement [`enterprise`](enterprise.md).

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique du système de réseau de télécommunications | `8` | PK, FK | Non | Clé primaire qui joue aussi le rôle de clé étrangère référençant `network_system.id` et `enterprise.id` |

## Relations

* **Hérite de (sous-type de) :** [`network_system`](network_system.md). La table `tlc_system` est une extension spécialisée de la table `network_system`.
* **Contient :** Bien qu'il ne soit pas lié directement via `tlc_system_id`, un système de télécommunications possède des actifs d'infrastructure par la colonne `enterprise_id` de la table `component`. Ces composants incluent souvent des sous-types spécialisés, tels que :
    * `tlc_network_component`

!!! tip "Où trouver le reste des données ?"
    Pour trouver le nom, la localisation géographique (`geometry`, `town`, `country`) ou les informations de propriété d'un système de réseau, vous devez joindre cette table à l'enregistrement `enterprise` qui partage le même `id`.

## Exemple de requête

Récupérez la liste de tous les systèmes électriques, avec leurs noms, communes et coordonnées spatiales, en joignant la table à son entité parente `network_system` - `enterprise` :

```sql
SELECT 
    tlc.id, 
    e.name, 
    e.town, 
    ST_AsText(e.geometry) as coordinates 
FROM 
    tlc_system tlc
JOIN 
    enterprise e ON tlc.id = e.id
WHERE 
    e.type = 'TLC_SYSTEM';