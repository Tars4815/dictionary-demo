# Table : `building_component`

!!! info "Nom différent dans l'interface web (GUI)"
    Dans le backend PostgreSQL, cette table s'appelle `building_component`, comme indiqué dans le titre de la page. Dans l'interface de l'application web, elle apparaît sous le nom **Principal structure**. Tous les alias figurent dans le [tableau de correspondance](../backend-to-gui.md).

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table stocke les caractéristiques structurelles, économiques et physiques des bâtiments, y compris les détails de construction, les types de matériaux et les dimensions. Dans l'architecture d'héritage de la base de données, elle joue le rôle de sous-type direct de la table [`component`](component.md). Elle ne stocke pas de colonnes descriptives redondantes : elle utilise à la place une clé primaire partagée pour hériter de tous les attributs de haut niveau (comme le nom, la localisation et la géométrie) de son enregistrement parent `component`.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique du composant de bâtiment | `42` | PK, FK | Non | Clé primaire qui joue aussi le rôle de clé étrangère référençant `component.id` |
| `principal` | BOOLEAN | Indique s'il s'agit du composant de bâtiment principal | `true` | - | Non | [...] |
| `subtype` | VARCHAR(255) | [...] | [...] | - | Non | [...] |
| `public_service_code` | VARCHAR(255) | [...] | [...] | - | Non | [...] |
| `heritage_tier` | VARCHAR(255) | [...] | [...] | - | Non | [...] |
| `year` | INTEGER | Année de construction | `1999` | - | Non |  |
| `quality` | VARCHAR(255) | Qualité globale | `GOOD` | - | Non | Valeurs possibles : POOR, GOOD, ACCEPTABLE, NOT_IDENTIFIABLE |
| `conservation` | VARCHAR(255) | État de conservation du bâtiment | `POORLY_MANTAINED` | CHECK | Non | Valeurs possibles : POORLY_MANTAINED, MODERATELY_MAINTAINED, WELL_MAINTAINED, NOT_IDENTIFIABLE |
| `retrofitting` | VARCHAR(255) | État du renforcement (rétrofit) | `NOT_IDENTIFIABLE` | CHECK | Non | Valeurs possibles : NONE, VERTICAL, HORIZONTAL, COMPLETE, NOT_IDENTIFIABLE, etc. |
| `regularity` | VARCHAR(255) | Régularité de la structure | `NOT_IDENTIFIABLE` | CHECK | Non | Valeurs possibles : NOT_REGULAR, COMPLETELY_REGULAR, etc. |
| `inhabitants` | INTEGER | Nombre d'habitants du bâtiment concerné | `6` | - | Non |  |
| `construction_cost` | INTEGER | Coût de construction | `500000` | - | Non |  |
| `economic_value` | INTEGER | Valeur économique | `1000000` | - | Non |  |
| `vertical_mat` | VARCHAR(255) | Matériau de construction des structures verticales | `NOT_IDENTIFIABLE` | CHECK | Non | Valeurs possibles : STEEL, WOOD, MASONRY_ADOBE, etc. |
| `horizontal_mat` | VARCHAR(255) | Matériau de construction des structures horizontales | `MASONRY_ADOBE` | CHECK | Non | Valeurs possibles : STEEL, WOOD, MASONRY_ADOBE, etc. |
| `roof_mat` | VARCHAR(255) | Matériau de l'élément de toiture | `NOT_IDENTIFIABLE` | CHECK | Non | Valeurs possibles : STEEL, WOOD, MASONRY_ADOBE, etc. |
| `build_position` | VARCHAR(255) | Position du bâtiment | `SINGLE_DETACHED` | CHECK | Non | Valeurs possibles : SINGLE_DETACHED, SEMI_DETACHED, ROW, NOT_IDENTIFICABLE |
| `ground_floor` | VARCHAR(255) | Typologie du rez-de-chaussée | `OPEN` | CHECK | Non | Valeurs possibles : OPEN, CLOSE, NOT_IDENTIFIABLE |
| `n_floors` | INTEGER | Nombre d'étages hors sol | `3` | - | Non |  |
| `floor_height` | INTEGER | Hauteur moyenne des étages | `4` | - | Non |  |
| `n_under_floors` | INTEGER | Nombre d'étages en sous-sol | `1` | - | Non |  |
| `floor_area` | INTEGER | Surface des planchers en mètres carrés | `1000` | - | Non |  |
| `usage` | VARCHAR(255) | [...] | [...] | - | Non | [...] |
| `foundation_typology` | VARCHAR(255) | Typologie des fondations | [...] | - | Non | [...] |
| `main_use` | VARCHAR(255) | Usage principal du bâtiment | [...] | - | Non | [...] |

## Relations

* **Hérite de (sous-type de) :** [`component`](component.md). La table `building_component` est une extension spécialisée de la table `component`.
* **Appartient à :** [`enterprise`](enterprise.md) (Un sous-type de composant est lié à une seule entreprise)
* **A plusieurs :** `damage` (Un sous-type de composant peut subir plusieurs dommages au fil du temps)

!!! tip "Où trouver le reste des données ?"
    Pour trouver le nom, la localisation géographique (`geometry`, `town`, `country`) ou les informations de propriété d'un composant de bâtiment, vous devez joindre cette table à l'enregistrement `component` qui partage le même `id`.

## Exemple de requête

Récupérez la liste de tous les composants de bâtiment, avec leurs noms, communes et coordonnées spatiales, en joignant la table à son entité parente `component` :

```sql
SELECT 
    bc.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    building_component bc
JOIN 
    component c ON bc.id = c.id
WHERE 
    c.component_kind = 'BUILDING_COMPONENT';
```
