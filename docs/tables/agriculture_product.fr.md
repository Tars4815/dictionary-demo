# Table : `agriculture_product`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table représente les produits agricoles. Dans l'architecture d'héritage de la base de données, elle joue le rôle de sous-type direct de la table [`component`](component.md). Elle ne stocke pas de colonnes descriptives redondantes : elle utilise à la place une clé primaire partagée pour hériter de tous les attributs de haut niveau (comme le nom, la localisation, le type de gestion et la géométrie) de son enregistrement parent `component`.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique du produit agricole | `42` | PK, FK | Non | Clé primaire qui joue aussi le rôle de clé étrangère référençant `component.id` |
| `average_invested` | BIGINT | [...] | [...] | - | Non | [...] |
| `expected_yield` | BIGINT | [...] | [...] | - | Non | [...] |
| `gate_price` | BIGINT | [...] | [...] | - | Non | [...] |
| `year_production` | BIGINT | [...] | [...] | - | Non | [...] |
| `subtype` | VARCHAR | [...] | [...] | - | Non | [...] |

## Relations

* **Hérite de (sous-type de) :** [`component`](component.md). La table `agriculture_product` est une extension spécialisée de la table `component`.
* **A des sous-types (héritage) :** Les tables suivantes héritent de `agriculture_product` et partagent son `id` :
    * [`crop`](crop.md)
    * [`stored`](stored.md)
* **Appartient à :** [`enterprise`](enterprise.md) (Un sous-type de composant est lié à une seule entreprise)
* **A plusieurs :** `damage` (Un sous-type de composant peut subir plusieurs dommages au fil du temps)

!!! tip "Où trouver le reste des données ?"
    Pour trouver le nom, la localisation géographique (`geometry`, `town`, `country`) ou les informations de propriété d'un produit agricole, vous devez joindre cette table à l'enregistrement `component` qui partage le même `id`.

## Exemple de requête

Récupérez la liste de tous les produits agricoles, avec leurs noms, communes et coordonnées spatiales, en joignant la table à son entité parente `enterprise` :

```sql
SELECT 
    ap.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    agriculture_product ap
JOIN 
    component c ON ap.id = c.id
WHERE 
    c.component_kind  = 'AGRICULTURE_PRODUCT';
```
