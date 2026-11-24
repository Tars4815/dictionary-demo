# Table : `crop`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table représente les cultures. Dans l'architecture d'héritage de la base de données, elle joue le rôle de sous-type direct de la table [`agriculture_product`](agriculture_product.md). Elle ne stocke pas de colonnes descriptives redondantes : elle utilise à la place une clé primaire partagée pour hériter de tous les attributs de haut niveau (comme le nom, la localisation, le type de gestion et la géométrie) de son enregistrement parent `component`.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique de l'enregistrement de la culture | `42` | PK, FK | Non | Clé primaire qui joue aussi le rôle de clé étrangère référençant `agriculture_product.id` puis `component.id` |
| `area_planted` | BIGINT | [...] | [...] | - | Non | [...] |
| `category` | VARCHAR | [...] | [...] | - | Non | [...] |
| `growth` | VARCHAR | [...] | [...] | - | Non | [...] |
| `duration` | VARCHAR | [...] | [...] | - | Non | [...] |

## Relations

* **Hérite de (sous-type de) :** [`agriculture_product`](agriculture_product.md). La table `crop` est une extension spécialisée de la table `agriculture_product`.
* **Appartient à :** [`enterprise`](enterprise.md) (Un sous-type de composant est lié à une seule entreprise)
* **A plusieurs :** `damage` (Un sous-type de composant peut subir plusieurs dommages au fil du temps)

!!! tip "Où trouver le reste des données ?"
    Pour trouver le nom, la localisation géographique (`geometry`, `town`, `country`) ou les informations de propriété d'une culture, vous devez joindre cette table à l'enregistrement `component` qui partage le même `id`.

## Exemple de requête

Récupérez la liste de toutes les cultures, avec leurs noms, communes et coordonnées spatiales, en joignant la table à son entité parente `component` :

```sql
SELECT
    c.id,
    c.area_planted,
    c.category,
    ap.year_production 
FROM 
    crop c join agriculture_product ap on c.id = ap.id 
where ap.subtype = 'CROP'
```