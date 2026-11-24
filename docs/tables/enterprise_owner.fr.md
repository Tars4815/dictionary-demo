# Table : `enterprise_owner`

!!! warning "Traduction assistée par IA"
    Cette page a été traduite avec l'assistance de l'intelligence artificielle et peut contenir des erreurs. La version anglaise fait foi. Les noms des tables et des attributs sont identiques dans toutes les langues car ils correspondent à ceux de l'implémentation PostgreSQL.

**Description (FR) :** Cette entité sert de table de liaison pour la relation plusieurs-à-plusieurs entre [`enterprise`](enterprise.md) et [`owner`](owner.md).

## Structure des colonnes

| Colonne | Type de données | Définition | Exemple de valeur | Contrainte ? | Géométrie ? | Commentaires |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `enterprise_id` | BIGINT | Identifiant de l'entreprise | `3` | FK | Non | Référence la table `enterprise` |
| `owner_id` | BIGINT | Identifiant du propriétaire | `8` | FK | Non | Référence la table `owner` |


