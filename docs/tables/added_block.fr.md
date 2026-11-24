# Table : `added_block`

!!! info "Nom différent dans l'interface web (GUI)"
    Dans le backend PostgreSQL, cette table s'appelle `added_block`, comme indiqué dans le titre de la page. Dans l'interface de l'application web, elle apparaît sous le nom **Added block**. Tous les alias figurent dans le [tableau de correspondance](../backend-to-gui.md).

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table représente les blocs ajoutés aux bâtiments. Dans l'architecture d'héritage de la base de données, elle joue le rôle de sous-type direct de la table [`component`](component.md). Elle ne stocke pas de colonnes descriptives redondantes : elle utilise à la place une clé primaire partagée pour hériter de tous les attributs de haut niveau (comme le nom, la localisation, le type de gestion et la géométrie) de son enregistrement parent `component`.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique du bloc ajouté | `42` | PK, FK | Non | Clé primaire qui joue aussi le rôle de clé étrangère référençant `component.id` |
| `position` | VARCHAR | [...] | `EXTERNAL` | - | Non | [...] |
| `vertical_mat` | VARCHAR | [...] | [...] | - | Non | [...] |
| `horizontal_mat` | VARCHAR | [...] | [...] | - | Non | [...] |
| `n_floor` | BIGINT | Nombre d'étages du bloc ajouté | `2` | - | Non | [...] |
| `total_height` | BIGINT | Hauteur totale du bloc ajouté en [unité de mesure] | `200` | - | Non | [...] |
| `floor_surface` | BIGINT | Surface totale des planchers du bloc ajouté en [unité de mesure] | `200` | - | Non | [...] |
| `floor_height` | BIGINT | Hauteur totale des étages du bloc ajouté en [unité de mesure] | `200` | - | Non | [...] |
| `function` | VARCHAR | [...] | [...] | - | Non | [...] |
| `previous_survey` | VARCHAR | [...] | [...] | - | Non | [...] |

## Relations

* **Hérite de (sous-type de) :** [`component`](component.md). La table `added_block` est une extension spécialisée de la table `component`.
* **Appartient à :** [`enterprise`](enterprise.md) (Un sous-type de composant est lié à une seule entreprise)
* **A plusieurs :** `damage` (Un sous-type de composant peut subir plusieurs dommages au fil du temps)

!!! tip "Où trouver le reste des données ?"
    Pour trouver le nom, la localisation géographique (`geometry`, `town`, `country`) ou les informations de propriété d'un enregistrement added_block, vous devez joindre cette table à l'enregistrement `component` qui partage le même `id`.

## Exemple de requête

Récupérez la liste de tous les blocs ajoutés, avec leurs noms, communes et coordonnées spatiales, en joignant la table à son entité parente `component` :

```sql
SELECT 
    ab.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    added_block ab
JOIN 
    component c ON ab.id = c.id
WHERE 
    c.component_kind  = 'ADDED_BLOCK';
```