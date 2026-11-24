# Table : `business`

!!! info "Nom différent dans l'interface web (GUI)"
    Dans le backend PostgreSQL, cette table s'appelle `business`, comme indiqué dans le titre de la page. Dans l'interface de l'application web, elle apparaît sous le nom **Economic Activities - Business**. Tous les alias figurent dans le [tableau de correspondance](../backend-to-gui.md).

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table représente les entreprises commerciales. Dans l'architecture d'héritage de la base de données, elle joue le rôle de sous-type direct de la table [`enterprise`](enterprise.md). Elle ne stocke pas de colonnes descriptives redondantes : elle utilise à la place une clé primaire partagée pour hériter de tous les attributs de haut niveau (comme le nom, la localisation, le type de gestion et la géométrie) de son enregistrement parent `enterprise`.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique de l'enregistrement de l'entreprise commerciale | `8` | PK, FK | Non | Clé primaire qui joue aussi le rôle de clé étrangère référençant `enterprise.id` |
| `share_capital` | BIGINT | Valeur monétaire totale des fonds de la société | [...] | - | Non | [...] |
| `nace_section` | VARCHAR | Classification de premier niveau de l'activité économique principale de l'entreprise commerciale, selon la norme NACE | [...] | - | Non | [...] |

## Relations

* **Hérite de (sous-type de) :** [`enterprise`](enterprise.md). La table `business` est une extension spécialisée de la table `enterprise`.
* **Contient :** Bien qu'il ne soit pas lié directement via `business_id`, un système de réseau possède des actifs d'infrastructure par la colonne `enterprise_id` de la table `component`. Ces composants incluent souvent des sous-types spécialisés, tels que :
    * `business_operations`

!!! tip "Où trouver le reste des données ?"
    Pour trouver le nom, la localisation géographique (`geometry`, `town`, `country`) ou les informations de propriété d'un système de réseau, vous devez joindre cette table à l'enregistrement `enterprise` qui partage le même `id`.

## Exemple de requête

Récupérez la liste de tous les enregistrements d'entreprises commerciales, avec leurs noms, communes et coordonnées spatiales, en joignant la table à son entité parente `enterprise` :

```sql
SELECT 
    b.id, 
    e.name, 
    e.town, 
    ST_AsText(e.geometry) as coordinates 
FROM 
    business b
JOIN 
    enterprise e ON b.id = e.id
WHERE 
    e.type = 'BUSINESS';
```