# Table : `network_service`

!!! info "Nom différent dans l'interface web (GUI)"
    Dans le backend PostgreSQL, cette table s'appelle `network_service`, comme indiqué dans le titre de la page. Dans l'interface de l'application web, elle apparaît sous le nom **Telecom service/Electrical service/Transport service**. Tous les alias figurent dans le [tableau de correspondance](../backend-to-gui.md).

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table représente les composants de type service de réseau. Dans l'architecture d'héritage de la base de données, elle joue le rôle de sous-type direct de la table [`component`](component.md). Elle ne stocke pas de colonnes descriptives redondantes : elle utilise à la place une clé primaire partagée pour hériter de tous les attributs de haut niveau (comme le nom, la localisation, le type de gestion et la géométrie) de son enregistrement parent `component`.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique du composant de type service de réseau | `42` | PK, FK | Non | Clé primaire qui joue aussi le rôle de clé étrangère référençant `component.id` |
| `value` | BIGINT | [...] | [...] | - | Non | - |
| `service` | VARCHAR | [...] | [...] | - | Non | - |
| `service_user` | VARCHAR | [...] | [...] | - | Non | - |

## Relations

* **Hérite de (sous-type de) :** [`component`](component.md). La table `network_service` est une extension spécialisée de la table `component`.
* **Appartient à :** [`enterprise`](enterprise.md) (Un sous-type de composant est lié à une seule entreprise)
* **A plusieurs :** `damage` (Un sous-type de composant peut subir plusieurs dommages au fil du temps)

!!! tip "Où trouver le reste des données ?"
    Pour trouver le nom, la localisation géographique (`geometry`, `town`, `country`) ou les informations de propriété d'un enregistrement network_service, vous devez joindre cette table à l'enregistrement `component` qui partage le même `id`.

## Exemple de requête

Récupérez la liste de tous les services de réseau, avec leurs noms, communes et coordonnées spatiales, en joignant la table à son entité parente `component` :

```sql
SELECT 
    ns.id, 
    c.name, 
    c.town, 
    ST_AsText(c.geometry) as coordinates 
FROM 
    network_service ns
JOIN 
    component c ON ns.id = c.id
```