# Table : `building_functionality`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette table représente la fonctionnalité des bâtiments pour les composants. Dans l'architecture d'héritage de la base de données, elle joue le rôle de sous-type direct de la table [`component`](component.md). Elle ne stocke pas de colonnes descriptives redondantes : elle utilise à la place une clé primaire partagée pour hériter de tous les attributs de haut niveau (comme le nom, la localisation, le type de gestion et la géométrie) de son enregistrement parent `component`.

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | BIGINT | Identifiant unique de la fonctionnalité du composant de bâtiment | `42` | PK, FK | Non | Clé primaire qui joue aussi le rôle de clé étrangère référençant `component.id` |
| `floor_number` | BIGINT | Nombre d'étages | `2` | - | Non | - |

[...]