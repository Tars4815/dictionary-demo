# Table : `fixed_asset`

!!! info "Nom différent dans l'interface web (GUI)"
    Dans le backend PostgreSQL, cette table s'appelle `fixed_asset`, comme indiqué dans le titre de la page. Dans l'interface de l'application web, elle apparaît sous le nom **Elements**. Tous les alias figurent dans le [tableau de correspondance](../backend-to-gui.md).

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table représente les composants de type immobilisation. Dans l'architecture d'héritage de la base de données, elle joue le rôle de sous-type direct de la table [`component`](component.md). Elle ne stocke pas de colonnes descriptives redondantes : elle utilise à la place une clé primaire partagée pour hériter de tous les attributs de haut niveau (comme le nom, la localisation, le type de gestion et la géométrie) de son enregistrement parent `component`.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique du composant de type immobilisation | `42` | PK, FK | Non | Clé primaire qui joue aussi le rôle de clé étrangère référençant `component.id` |

## Relations

* **Hérite de (sous-type de) :** [`component`](component.md). La table `fixed_asset` est une extension spécialisée de la table `component`.
* **A des sous-types (héritage) :** Les tables suivantes héritent de `fixed_asset` et partagent son `id` :
    * [`infrastructure`](infrastructure.md)
    * [`land`](land.md)
    * [`machinery`](machinery.md)
    * [`material`](material.md)
* **Appartient à :** [`enterprise`](enterprise.md) (Un sous-type de composant est lié à une seule entreprise)
* **A plusieurs :** `damage` (Un sous-type de composant peut subir plusieurs dommages au fil du temps)

!!! tip "Où trouver le reste des données ?"
    Pour trouver le nom, la localisation géographique (`geometry`, `town`, `country`) ou les informations de propriété d'un enregistrement fixed_asset, vous devez joindre cette table à l'enregistrement `component` qui partage le même `id`.

## Exemple de requête

Récupérez la liste de toutes les immobilisations, avec leurs noms, communes et coordonnées spatiales, en joignant la table à son entité parente `enterprise` :

```sql
SELECT 
    fa.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    fixed_asset
JOIN 
    component c ON fa.id = c.id
WHERE 
    c.component_kind  = 'FIXED_ASSET';
```