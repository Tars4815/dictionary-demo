# Table : `network_system`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table représente les systèmes de réseau d'infrastructure (p. ex. réseaux de transport, d'électricité ou de télécommunications). Dans l'architecture d'héritage de la base de données, elle joue le rôle de sous-type direct de la table [`enterprise`](enterprise.md). Elle ne stocke pas de colonnes descriptives redondantes : elle utilise à la place une clé primaire partagée pour hériter de tous les attributs de haut niveau (comme le nom, la localisation, le type de gestion et la géométrie) de son enregistrement parent `enterprise`.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique du système de réseau | `8` | PK, FK | Non | Clé primaire qui joue aussi le rôle de clé étrangère référençant `enterprise.id` |

## Relations

* **Hérite de (sous-type de) :** [`enterprise`](enterprise.md). La table `network_system` est une extension spécialisée de la table `enterprise`.
* **A des sous-types (héritage) :** Les tables suivantes héritent de `network_system` (et, par son intermédiaire, de `enterprise`) et partagent son `id` :
    * [`electrical_system`](electrical_system.md)
    * [`tlc_system`](tlc_system.md)
    * [`transport_system`](transport_system.md)
* **Contient :** Bien qu'il ne soit pas lié directement via `network_system_id`, un système de réseau possède des actifs d'infrastructure par la colonne `enterprise_id` de la table `component`. Ces composants incluent souvent des sous-types spécialisés, tels que :
    * `transport_network_component`
    * `electrical_network_component`
    * `tlc_network_component`
    * `network_service`

!!! tip "Où trouver le reste des données ?"
    Pour trouver le nom, la localisation géographique (`geometry`, `town`, `country`) ou d'autres informations sur un système de réseau, vous devez joindre cette table à l'enregistrement `enterprise` qui partage le même `id`.

## Exemple de requête

Récupérez la liste de tous les systèmes de réseau, avec leurs noms, communes et coordonnées spatiales, en joignant la table à son entité parente `enterprise` :

```sql
SELECT 
    n.id, 
    e.name, 
    e.town, 
    e.type,
    ST_AsText(e.geometry) as coordinates 
FROM 
    network_system n
JOIN 
    enterprise e ON n.id = e.id;
```
